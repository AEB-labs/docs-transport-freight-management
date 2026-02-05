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

# Authentication

<Authentication />

<Callout icon="❗️" theme="error">
  **You cannot use regular Carrier Connect users for API requests!** Instead you will need a special API user to transmit API requests, which usually starts with _WSM_.
</Callout>

The login data must be base 64–encoded. The password is written out, so this is why we require using HTTPS encryption and the data cannot be intercepted by unauthorized parties.

**Example:**

The string "API_TEST@APITEST:API_TEST2024", when encoded in base 64, yields “QVBJX1RFU1RAQVBJVEVTVDpBUElfVEVTVDIwMjQ=".

The following line would therefore be added to the HTTP header:
Authorization: Basic QVBJX1RFU1RAQVBJVEVTVDpBUElfVEVTVDIwMjQ

## IP of the AEB data center

194.175.186.2

## Port

HTTPS URLs use port **443** by default.

# Endpoints

You have to replace `<carrier_connect_system>` with the system you want to connect (e.g. demo1cai, test2cai, prod1cai).

| \<carrier_connect_system> | Description                             |
| :------------------------ | :-------------------------------------- |
| test2cai                  | Test environment                        |
| prod1cai                  | Productive environment                  |
| prod2cai                  | Productive environment (First Customer) |

<br />

## REST (OpenApi)

https://rz3.aeb.de/test2cai/rest/openapi.json

## SOAP

https://rz3.aeb.de/test2cai/servlet/bf/DLCarrierBF?WSDL
https://rz3.aeb.de/test2cai/servlet/bf/doc/DLCarrierBF/de/aeb/xnsg/dl/bf/IDLCarrierBF.html

<br />

<Callout icon="💡" theme="default">
  ### The API is only available via Secure Socket Layer (SSL).
</Callout>

# Test Credentials

Before you can start using the Carrier Connect API, you need a user and a password. AEB will provide them to you.

**If you do not have your own client yet, you can use the following credentials to test the API:**

| Parameter              | Value        |
| :--------------------- | :----------- |
| Carrier Connect System | demo1cai     |
| Client                 | APITEST      |
| User                   | API_TEST     |
| Password               | API_TEST2024 |

<Callout icon="❗️" theme="error">
  The client "APITEST" is intended for basic connectivity testing and is used by different users. Don't use it with sensitive data.
</Callout>
