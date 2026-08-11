---
title: Carrier Connect API Essentials
excerpt: >-
  Base URL, authentication, the request envelope, the response/error model, and
  the create-then-poll workflow you need before your first call — including the
  asynchronous and idempotency behaviour that most integrations get wrong.
deprecated: false
hidden: false
metadata:
  robots: index
---
Carrier Connect is AEB's multi-carrier shipping system. You use it to **create, validate, update, and cancel shipments and pickups**, generate **carrier labels and customs documents**, and handle **returns and hazardous goods**. Operations are RPC-style calls exposed over REST as JSON or XML, and also over SOAP.

This page is the one-page orientation. Read it before your first call — it covers the four things that aren't obvious from the individual endpoint pages: **how errors are returned, how asynchronous processing works, why `createShipment` isn't idempotent, and the order to call things in.**

<Callout icon="📘" theme="info">
  ### This page summarises; the linked pages are authoritative

  Where a block below is marked _Full reference: …_, the linked page owns the detail and wins in case of doubt. The `openapi.json` of your installation is authoritative for every field.
</Callout>

## Base URL and endpoints

```text
https://rz3.aeb.de/{installation}/rest/DLCarrierBFBean/{operation}
```

For example: `https://rz3.aeb.de/prod1cai/rest/DLCarrierBFBean/createShipment`.

All operations are `POST`. The `installation` segment identifies your environment — see [Setting up your environment](doc:setting-up-your-environment). The full machine-readable contract for every operation is the **OpenAPI 3.1 spec** at:

```text
https://rz3.aeb.de/prod1cai/rest/openapi.json
```

That spec covers the whole installation; Carrier Connect operations are tagged `Shipping` and live under the `DLCarrierBFBean` bean.

## Authentication

Authenticate in the request `Authorization` **header** — credentials never go in the request body. Carrier Connect (`DLCarrierBFBean`) operations accept **either** scheme:

- **HTTP Basic** — `Authorization: Basic base64(USER@CLIENT:PASSWORD)`. The client is part of the user name; without the `@CLIENT` part the request fails with `401 … no @ for client found`.
- **Bearer token** — call `GET /logon/authToken` once with Basic credentials and `Accept: text/plain` (or `POST /logon/user` with `userName` / `password` / `clientName`), then send the returned token as `Authorization: Bearer <token>` on subsequent calls.

Always send `Accept: application/json` on the operations themselves, so error responses come back as JSON rather than an HTML error page. The one exception is `GET /logon/authToken`, which returns plain text and answers `406 Not Acceptable` to `Accept: application/json`.

The globally-declared `X-XNSG_WEB_TOKEN` header is the browser/web **session token**, not an API integration path — it is rejected on these operations with `401 Authentication required`.

See [Setting up your environment](doc:setting-up-your-environment) for obtaining credentials and tokens for your installation.

{/* Author note: auth verified live on test1cai — Basic OK, Bearer OK (token from GET /logon/authToken), X-XNSG_WEB_TOKEN rejected ("Authentication required").
     Re-verified on demo1cai: Basic without @CLIENT returns 401 "invalid syntax in 'userName' - no @ for client found"; GET /logon/authToken with Accept: application/json returns 406.
     Doc-defect to fix at source: the OpenAPI spec under-declares — DLCarrierBFBean ops list BASIC_AUTH only and no bearer scheme is declared, yet Bearer works at the gateway. Add a bearer securityScheme and list it on these ops so the spec matches reality.
     Second spec defect: in DLCreateShipmentResponseDTO, hasWarnings and hasOnlyRetryableErrors both carry the description text of hasErrors.
     Third: clientSystemId is not marked required anywhere, but getShipments rejects a request without it (EMPTY_MANDATORY_FIELD, "Client system id not filled."). */}

<Callout icon="📘" theme="info">
  ### The "userName" field in the request body is not authentication

  It selects which roles the request runs under: if the user exists in user management or the connected LDAP, the request runs with that user's roles; if not, it falls back to the basic `I_EVERYONE` role. Actual authentication is always the header above.
</Callout>

_Full reference: [Setting up your environment](doc:setting-up-your-environment) — credentials, API users, systems, endpoints._

## Request and response format

Send `Content-Type: application/json` (or `application/xml`); set `Accept` to match.

Every request carries the same four optional top-level fields alongside its payload:

| Field                    | Purpose                                                                                                                                                                                          |
| :----------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `clientSystemId`         | Id of the sending host or ERP system (max. 20). Formally optional, but several operations reject the request without it — set it.                                                                 |
| `clientIdentCode`        | Client identification code (max. 10).                                                                                                                                                            |
| `userName`               | User who initiated the request in your system — role selection and logging, not authentication.                                                                                                   |
| `resultLanguageIsoCodes` | Ordered list of 2-letter ISO codes for the returned message texts. `en` and `de` are supported by default; translations fall back to the next language in the list. Leave it empty and Carrier Connect warns and uses English. |

## The shipment request envelope

Every `createShipment` call has three **required** top-level objects:

| Object          | Purpose                                                                                                                                  |
| :-------------- | :---------------------------------------------------------------------------------------------------------------------------------------- |
| `creationParms` | _Whether_ the shipment is created. Required member: `creationMode` = `VALIDATION_OK` (create only if validation passes) or `ALWAYS`.      |
| `shipment`      | The shipment data itself.                                                                                                                |
| `processParms`  | _What happens after_ creation — label preparation, label output, completion, pickup assignment.                                           |

`shipment` requires nine fields: `transactionId`, `referenceNumber1`, `shippingDate`, `contents`, `shippingPt` (sender address), `consignee` (recipient address), `carrierIdentCode`, `serviceCode`, `termsOfDeliveryCode`.

`processParms` requires six: `processMode`, `doCompletion`, `documentPrepareScope`, `documentOutputMode`, `documentOutputScope`, `workstationId`.

The full object is large and deeply nested — **use the OpenAPI spec as the source of truth** and the [The First Shipment](doc:the-first-shipment-v2) guide for a complete copy-paste example. Don't hand-build it from memory.

_Full reference: [Creation Parameters](doc:creation-parameters-v2), [Process Parameters](doc:process-parameters), [Important body fields](doc:important-header-fields)._

## Synchronous vs. asynchronous — this determines what you get back

`processParms.processMode.mode` — an object with a `mode` member, not a plain string — controls the single most important behaviour:

- **`BASIC`** (light path): label preparation runs asynchronously in a background job. The response only confirms the shipment was written to the database — the labels and any label-preparation errors are **not** in the response. You retrieve them afterwards with `syncShipments` or `getShipments`.
- **`EXTENDED`** (synchronous): the response does not return until label preparation is finished, so labels and preparation errors come back in-band. It uses more resources and reduces load-balancing benefit — use it only when you need an immediate, complete response.

These response fields are filled **only** in `EXTENDED` mode: `carrierShipmentNumber`, `carrierShipmentNumberReturn`, `accountInfo`, and parts of `packageResults[]`. `shipmentNumber` is filled in both.

<Callout icon="🚧" theme="warn">
  ### In BASIC mode, a successful createShipment response does not mean the label succeeded

  Always poll `syncShipments` / `getShipments` to confirm the operation result.
</Callout>

## How to read every response

Operations return HTTP 200 even for business errors. **Do not rely on the HTTP status code.** Instead, always inspect the body:

- `hasErrors` — `true` means the request could generally not be performed.
- `hasWarnings` — `true` means non-fatal issues. Not always non-fatal: see the `VALIDATION_OK` warning below.
- `hasOnlyRetryableErrors` — `true` means the errors signal a temporary problem, such as a locked resource; safe to retry.
- `messages[]` — each has a `messageType` (`ERROR` / `WARNING` / `INFO`), a machine-readable `messageIdentCode`, and human-readable `messageTexts[]`.
- `packageResults[]` — carries its own `hasErrors` / `messages[]` per package; check these too, not just the top level. On the validation path, package problems may be reported at shipment level instead, so never read an empty `packageResults[]` as "no package problems".

A real response to a deliberately empty `getShipments` request:

```json
{
  "hasErrors": true,
  "hasOnlyRetryableErrors": false,
  "hasWarnings": true,
  "messages": [
    {
      "messageType": "WARNING",
      "messageIdentCode": "I18N_WARNING",
      "messageTexts": [
        { "languageISOCode": "en", "text": "Language ISO Code is empty. Using language \"English\" for messages in response." }
      ]
    },
    {
      "messageType": "ERROR",
      "messageIdentCode": "EMPTY_MANDATORY_FIELD",
      "messageTexts": [
        { "languageISOCode": "en", "text": "Client system id not filled." }
      ]
    }
  ]
}
```

Branch on `messageIdentCode` (stable, language-independent), not on the message text.

_Full reference: [Error Handling](doc:error-handling-v2) — the complete message model and codes._

<Callout icon="🚧" theme="warn">
  ### With creationMode = VALIDATION\_OK, a warning also prevents creation

  `hasErrors = false` and `hasWarnings = true` then means **no shipment was created**. In this creation mode you must treat warnings as errors. This applies regardless of `doCompletion` — setting `doCompletion = true` only makes warnings more likely, because it raises the status the shipment must reach.

  Two consequences that surprise people:

  * In `EXTENDED` mode, label preparation runs before the creation decision is final, and a preparation problem can surface as a _warning_ rather than an error. Under `VALIDATION_OK` that warning is enough to discard the shipment — so a label problem can cost you the shipment record too.
  * Use `creationMode = ALWAYS` if you want the shipment kept for inspection when validation is incomplete.
</Callout>

## Idempotency and retries

`createShipment` is **not idempotent**. If a shipment with the same `shipment.transactionId` already exists, the call returns `messageIdentCode = SHIPMENT_RETRANSMISSION_ERROR` ("A shipping order with transaction ID '…' already exists. Retransmission is not possible.") — it does not return or update the existing shipment.

Because of this, a naive retry after a timeout (common with `EXTENDED` mode or network blips) will fail with that error. Handle it deliberately:

1. On a lost or uncertain response, call `getShipments` for your `transactionId` to check whether the shipment was in fact created.
2. Retry `createShipment` only if it was not.
3. Treat `SHIPMENT_RETRANSMISSION_ERROR` as "already created", not as a hard failure.

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

To take a shipment back, use `cancelShipment` (there is no `deleteShipment`); `deletePackage`, `deleteItem` and `deletePickup` operate on the smaller objects.

## Gotchas checklist

- [ ] Authenticate with `USER@CLIENT`, not just the user name.
- [ ] Check `hasErrors` / `hasWarnings` in the body — not the HTTP status.
- [ ] Also check `packageResults[].messages[]`, not only the top-level `messages[]`.
- [ ] Set `clientSystemId`; several operations reject the request without it.
- [ ] In `BASIC` mode, poll `syncShipments` / `getShipments` for labels and async errors.
- [ ] Give every shipment a unique `transactionId`; expect `SHIPMENT_RETRANSMISSION_ERROR` on duplicates.
- [ ] With `creationMode = VALIDATION_OK`, warnings alone mean nothing was created.
- [ ] Branch on `messageIdentCode`, not on message text.

## Where to go next

- [The First Shipment](doc:the-first-shipment-v2) — a complete, copy-paste `createShipment` call.
- [Creation Parameters](doc:creation-parameters-v2) and [Process Parameters](doc:process-parameters) — the `creationParms` / `processParms` options in full.
- [Error Handling](doc:error-handling-v2) — the complete message model and codes.
- [Sync and Get calls](doc:sync) — retrieving results, labels, and changes.
- [Code lists for quantity units](doc:code-lists-1) — the quantity unit abbreviations your host system must use.
- **OpenAPI spec** (`/rest/openapi.json`) — the authoritative schema for every field.
