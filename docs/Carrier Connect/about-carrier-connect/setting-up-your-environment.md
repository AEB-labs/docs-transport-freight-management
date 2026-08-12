---
title: Setting up your environment
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
<HTMLBlock>{`
<style>
  span.cm-s-neo {
    background-color: #f2f2f2;
    color: red;
  }
</style>
`}</HTMLBlock>

## Authentication

<Authentication />

<Callout icon="❗️" theme="error">
  **You cannot use regular Carrier Connect users for API requests!** Instead you will need a special API user to transmit API requests, which usually starts with _WSM_.
</Callout>

The login data must be base 64–encoded. The password is written out, so this is why we require using HTTPS encryption and the data cannot be intercepted by unauthorized parties.

**Example:**

The string "API_TEST@APITEST:API_TEST2024", when encoded in base 64, yields "QVBJX1RFU1RAQVBJVEVTVDpBUElfVEVTVDIwMjQ=".

The following line would therefore be added to the HTTP header:

```text
Authorization: Basic QVBJX1RFU1RAQVBJVEVTVDpBUElfVEVTVDIwMjQ=
```

<Callout icon="❗️" theme="error">
  ### Copy the trailing "=" as well

  It is part of the base 64 padding. Some servers reject an unpadded value.
</Callout>

Always send `Accept: application/json` as well, so that error responses come back as JSON rather than as an HTML error page.

### Firewall: IP subnetworks of the AEB data centers

Carrier Connect is reached over **HTTPS on port 443** only. If your firewall or proxy restricts outbound traffic, allow AEB's inbound web subnetworks:

```text
194.15.60.0/25
194.15.61.0/25
194.15.62.0/25
193.98.221.0/25
194.175.186.0/24
```

Allow **all five**, not the single IP address of the host you happen to call. AEB moves services between data centers, and a rule pinned to one address stops working on failover.

<Callout icon="💡" theme="default">
  ### The API is only available via Secure Socket Layer (SSL).

  Port 443. There is no plain-HTTP endpoint.
</Callout>

Two cases need more than the rows above, and both are covered by <a href="https://service.aeb.com/hc/en-us/articles/18380335264273-Public-IP-subnetworks-of-the-AEB-data-centers" target="_blank">Public IP subnetworks of the AEB data centers</a> — the maintained source, which wins over this page:

* **SFTP** (TCP 22), if you exchange EDI files with AEB — its own set of subnetworks.
* **AEB's outbound source IPs**, if your own firewall filters traffic coming *from* AEB.

## Systems

Every URL in this guide contains an `{installation}` placeholder. Replace it with the system you connect to:

| `{installation}` | Description                                                                     |
| :--------------- | :------------------------------------------------------------------------------ |
| demo1cai         | Demo system — shared, used for connectivity tests and the test credentials below |
| test2cai         | Test environment                                                                |
| prod1cai         | Productive environment                                                          |
| prod2cai         | Productive environment (First Customer)                                         |

## Endpoints

All Carrier Connect operations are `POST` calls under one base URL:

```text
https://rz3.aeb.de/{installation}/rest/DLCarrierBFBean/{operation}
```

For example: `https://rz3.aeb.de/demo1cai/rest/DLCarrierBFBean/createShipment`.

The complete list of operations, with every field, is under <Anchor label="API Reference" target="_blank" href="https://transport-freight-management.docs.developers.aeb.com/reference/addshipmentattachments">API Reference</Anchor>:

![](https://files.readme.io/0d25b222e8efc0e63dd67aa5780bb99393eb9f21c08226c1366d9c7a45a68e3d-image.png)

<br />

## Documentation

### REST (OpenApi)

```text
https://rz3.aeb.de/{installation}/rest/openapi.json
```

This is the authoritative machine-readable contract for every field. The file covers the whole installation — Carrier Connect operations are the ones tagged `Shipping`, under `DLCarrierBFBean`.

### SOAP

Carrier Connect is also available over SOAP. Use REST for new integrations; SOAP is there for existing ones.

```text
https://rz3.aeb.de/{installation}/servlet/bf/DLCarrierBF?WSDL
https://rz3.aeb.de/{installation}/servlet/bf/doc/DLCarrierBF/de/aeb/xnsg/dl/bf/IDLCarrierBF.html
```

## Optional: token authentication

Instead of sending Basic credentials on every call, you can exchange them once for a token:

```bash
curl -u 'USER@CLIENT:PASSWORD' \
  -H 'Accept: text/plain' \
  'https://rz3.aeb.de/{installation}/rest/logon/authToken'
```

Send the returned token as `Authorization: Bearer <token>` on subsequent calls.

<Callout icon="❗️" theme="error">
  ### This one call needs "Accept: text/plain"

  `/logon/authToken` returns the token as plain text. With `Accept: application/json` it answers `406 Not Acceptable`.
</Callout>

`POST /logon/user` (body: `userName`, `password`, `clientName`, optional `localeName`) is the alternative, and additionally returns the roles granted to the user.

<Callout icon="📘" theme="info">
  ### "X-XNSG\_WEB\_TOKEN" is not an API integration path

  The header is declared globally in the OpenAPI file, but Carrier Connect operations reject it with `401 Authentication required`. Use Basic or Bearer.
</Callout>

## Test Credentials

Before you can start using the Carrier Connect API, you need a user and a password. AEB will provide them to you.

<Callout icon="❗️" theme="error">
  The client "APITEST" is intended for **basic connectivity testing** and is used by different users. **This is not intended to use for API integration tests**. Don't use it with sensitive data.
</Callout>

**If you do not have your own client yet, you can use the following credentials to test the API:**

| Parameter              | Value        |
| :--------------------- | :----------- |
| Carrier Connect System | demo1cai     |
| Client                 | APITEST      |
| User                   | API_TEST     |
| Password               | API_TEST2024 |

## Check your setup

Confirm that credentials and endpoint work before you build a shipment:

```bash
curl -s -u 'API_TEST@APITEST:API_TEST2024' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -X POST 'https://rz3.aeb.de/demo1cai/rest/DLCarrierBFBean/getShipments' \
  -d '{}'
```

How to read the outcome:

| Response                              | Meaning                                                                    |
| :------------------------------------ | :------------------------------------------------------------------------- |
| `401` with "no @ for client found"    | The `USER@CLIENT` format is missing the client part                        |
| `401 Authentication required`         | Credentials rejected                                                       |
| `403 Access denied to method …`       | Authentication worked; the user lacks the role for that operation          |
| `200` with a JSON body                | You are through — continue with [Carrier Connect API Essentials](doc:start-here-carrier-connect-api-essentials) |

Note that the `200` body of this deliberately empty request contains `"hasErrors": true`. That is not a setup problem — it is the first thing the next page explains.
