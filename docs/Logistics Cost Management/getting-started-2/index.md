---
title: Getting started
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: You have to set up your enfironment. So choose your context.
  pages:
    - type: basic
      slug: setting-up-your-envorinment-any-platform-1
      title: Setting up your envorinment (any platform) LCM
    - type: basic
      slug: setting-up-your-sap-s4erp-envorinment-2
      title: Setting up your SAP S4/ERP envorinment (LCM)
---
## Playing around with the API

If you just want to play around with the API Methods of  Logistics Cost Management, you can use one of the following options.

## Readme.io

* Go to the [API Reference](https://transport-freight-management.docs.developers.aeb.com/reference/acknowledgechangedsettlements) of this documentation and navigate to the *Logistics Cost Management* section.
* Authenticate yourself by entering "*user*@*client*" and your password into the auth popup, right next to the *try it* button.

## Swagger

* Authenticate yourself by clicking the Authorize button at the top of the page.
* Go to the [Swagger UI of the demo engine](https://rz3.aeb.de/demo1billing/swagger/).

## Manually setting up the API

The Logistics Cost Management API methods can be found at: 

## REST (OpenApi)

`*ENGINE_URL*/rest/openapi.json` (e.g. `https://rz3.aeb.de/demo1billing/rest/openapi.json`)

## SOAP

Business facade for the Billing Engine\
`*ENGINE_URL*/servlet/bf/BillingBF?WSDL` (e.g. `https://rz3.aeb.de/demo1billing/servlet/bf/BillingBF?WSDL`)

Business facade for rates in the Billing Engine\
`*ENGINE_URL*/servlet/bf/RateBF?WSDL` (e.g. `https://rz3.aeb.de/demo1billing/servlet/bf/RateBF?WSDL`)

Business facade interface, handling requests for external invoice project\
`*ENGINE_URL*/servlet/bf/ExternalInvoiceBF?WSDL` (e.g. `https://rz3.aeb.de/demo1billing/servlet/bf/ExternalInvoiceBF?WSDL`)

For Authentication see: [Credentials](https://transport-freight-management.docs.developers.aeb.com/docs/setting-up-your-environment#credentials)
