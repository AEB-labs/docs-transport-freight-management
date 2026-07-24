---
title: 'Start Here: Carrier Connect API Essentials'
excerpt: >-
  Base URL, authentication, the request envelope, the response/error model, and
  the create-then-poll workflow you need before your first call — including the
  asynchronous and idempotency behaviour that most integrations get wrong.
deprecated: false
hidden: true
metadata:
  robots: index
---
Carrier Connect is AEB's multi-carrier shipping system. You use it to **create, validate, update, and cancel shipments and pickups**, generate **carrier labels and customs documents**, and handle **returns and hazardous goods**. Operations are RPC-style calls exposed over REST as JSON or XML.

This page is the one-page orientation. Read it before your first call — it covers the four things that aren't obvious from the individual endpoint pages: **how errors are returned, how asynchronous processing works, why&#x20;**`createShipment`**&#x20;isn't idempotent, and the order to call things in.**

## Base URL and endpoints

```text
https://rz3.aeb.de/{installation}/rest/DLCarrierBFBean/{operation}
```

For example: `https://rz3.aeb.de/prod1cai/rest/DLCarrierBFBean/createShipment`.

`{installation}` identifies your environment (e.g. a test vs. production installation). The full machine-readable contract for every operation is the **OpenAPI 3.1 spec** at:

```text
https://rz3.aeb.de/prod1cai/rest/openapi.json
```

That spec covers the whole Transport & Freight Management platform; Carrier Connect operations are tagged `Shipping` and live under the `DLCarrierBFBean` bean.

## Authentication

Authenticate in the request `Authorization`**&#x20;header** — credentials never go in the request body. Carrier Connect (`DLCarrierBFBean`) operations accept **either** scheme:

- **HTTP Basic** — `Authorization: Basic base64(user:password)`
- **Bearer token** — call `GET /logon/authToken` once with Basic credentials (or `POST /logon/user` with `userName` / `password` / `clientName`), then send the returned token as `Authorization: Bearer <token>` on subsequent calls.

Always send `Accept: application/json` too, so error responses come back as JSON rather than an HTML error page.

The globally-declared `X-XNSG_WEB_TOKEN` header is the browser/web **session token**, not an API integration path — it is rejected on these operations.

See [Setting up your environment](doc:setting-up-your-environment) for obtaining credentials and tokens for your installation.

{/* Author note: auth verified live on test1cai — Basic OK, Bearer OK (token from GET /logon/authToken), X-XNSG_WEB_TOKEN rejected ("Authentication required").
     Doc-defect to fix at source: the OpenAPI spec under-declares — DLCarrierBFBean ops list BASIC_AUTH only and no bearer scheme is declared, yet Bearer works at the gateway. Add a bearer securityScheme and list it on these ops so the spec matches reality. */}

<Callout icon="📘" theme="info">
  ### The `userName` field in the request body is **not** authentication. It selects which roles the request runs under: if the user exists in user management or the connected LDAP, the request runs with that user's roles; if not, it falls back to the basic `I_EVERYONE` role. Actual authentication is always the header above.
</Callout>

## Request and response format

- Send `Content-Type: application/json` (or `application/xml`); set `Accept` to match.
- Optionally set `resultLanguageIsoCodes` (ordered list of 2-letter ISO codes) to control the language of returned messages. Translations fall back to the next language in the list.

## The shipment request envelope

Every `createShipment` call has three **required** top-level objects plus optional identifiers:

| Object          | Purpose                                                                                                              |
| --------------- | -------------------------------------------------------------------------------------------------------------------- |
| `creationParms` | _Whether_ the shipment is created — `creationMode` = `VALIDATION_OK` (create only if validation passes) or `ALWAYS`. |
| `shipment`      | The shipment data itself (see below).                                                                                |
| `processParms`  | _What happens after_ creation — label preparation, label output, completion, pickup assignment.                      |

At minimum, `shipment` requires: `transactionId`, `referenceNumber1`, `shippingDate`, `contents`, `shippingPt` (sender address), `consignee` (recipient address), `carrierIdentCode`, `serviceCode`, and `termsOfDeliveryCode`. The full object is large and deeply nested — **use the OpenAPI spec as the source of truth** and the [The First Shipment](doc:the-first-shipment-v2) guide for a complete copy-paste example. Don't hand-build it from memory.

## Synchronous vs. asynchronous — this determines what you get back

`processParms.processMode` controls the single most important behaviour:

- `BASIC`**&#x20;(light path):** Label preparation runs **asynchronously** in a background job. The response **only confirms the shipment was written to the database** — the labels and any label-preparation errors are **not in the response**. You retrieve them afterwards with `syncShipments` or `getShipments`.
- `EXTENDED`**&#x20;(synchronous):** The response does not return until label preparation is finished, so labels and preparation errors come back in-band. It uses more resources and reduces load-balancing benefit — use it only when you need an immediate, complete response.

<Callout icon="🚧" theme="warning">
  ### In `BASIC` mode, a successful `createShipment` response does **not** mean the label succeeded. Always poll `syncShipments`/`getShipments` to confirm the operation result.
</Callout>

## How to read every response

Operations return **HTTP&#x20;**`200` even for business errors. **Do not rely on the HTTP status code.** Instead, always inspect the body:

- `hasErrors` — `true` means the request could generally not be performed.
- `hasWarnings` — `true` means non-fatal issues.
- `hasOnlyRetryableErrors` — `true` means the errors are transient (e.g. locked data); safe to retry.
- `messages[]` — each has a `messageType` (`ERROR` / `WARNING` / `INFO`), a machine-readable `messageIdentCode`, and human-readable `messageTexts[]`.
- `packageResults[]` — carries its own `hasErrors` / `messages[]` **per package**; check these too, not just the top level.

```json
{
  "hasErrors": true,
  "hasOnlyRetryableErrors": false,
  "hasWarnings": false,
  "messages": [
    {
      "messageType": "ERROR",
      "messageIdentCode": "PICKUP_NOT_FOUND_ERROR",
      "messageTexts": [
        { "languageISOCode": "en", "text": "Unable to find pickup for Pickup no. …" }
      ]
    }
  ]
}
```

Branch on `messageIdentCode` (stable, language-independent), not on the message text.

<Callout icon="🚧" theme="warning">
  ### One special case: with `processParms.doCompletion = true` **and** `creationParms.creationMode = VALIDATION_OK`, a response of `hasErrors = false` **and** `hasWarnings = true` means **no shipment was created**. In this combination you must treat warnings as errors.
</Callout>

## Idempotency and retries

`createShipment` is **not idempotent**. If a shipment with the same `shipment.transactionId` already exists, the call returns an **error** — it does not return or update the existing shipment. `transactionId` is your unique reference to the business transaction in your system, and duplicates are rejected.

Because of this, a naive retry after a timeout (common with `EXTENDED` mode or network blips) will fail with a duplicate error. Handle it deliberately:

1. On a lost/uncertain response, call `getShipments` for your `transactionId` to check whether the shipment was in fact created.
2. Retry `createShipment` only if it was not.
3. Treat a duplicate-exists error as "already created," not as a hard failure.

## The typical workflow

```text
validateShipment   (optional) → check the shipment can be processed
      │
createShipment     → create; processParms drives label prep/output/completion
      │
syncShipments /    → in BASIC mode, poll for async label results and errors
getShipments
      │
processShipment    → add packages, (re)print documents, complete the shipment
      │
createPickup       → assign shipments to a pickup and manifest to the carrier
```

## Gotchas checklist

- [ ] Check `hasErrors` / `hasWarnings` in the body — **not** the HTTP status.
- [ ] Also check `packageResults[].messages[]`, not only the top-level messages.
- [ ] In `BASIC` mode, poll `syncShipments`/`getShipments` for labels and async errors.
- [ ] Give every shipment a unique `transactionId`; expect an error on duplicates.
- [ ] `doCompletion = true` + `VALIDATION_OK` + warnings-only ⇒ nothing was created.
- [ ] Branch on `messageIdentCode`, not on message text.

## Where to go next

- [Setting up your environment](doc:setting-up-your-environment) — credentials, tokens, installations.
- [The First Shipment](doc:the-first-shipment-v2) — a complete, copy-paste `createShipment` call.
- [Creation Parameters](doc:creation-parameters-v2) and [Process Parameters](doc:process-parameters) — the `creationParms` / `processParms` options in full.
- [Error Handling](doc:error-handling-v2) — the complete message model and codes.
- [Sync and Get calls](doc:sync) — retrieving results, labels, and changes.
- <Anchor target="_blank" href="https://rz3.aeb.de/prod1cai/rest/openapi.json">**OpenAPI spec**</Anchor> (`/rest/openapi.json`) — the authoritative schema for every field.

<br />
