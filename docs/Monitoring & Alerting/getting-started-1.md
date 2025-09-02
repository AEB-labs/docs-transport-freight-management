---
title: Getting Started
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
Want to connect AEB Monitoring & Alerting (M\&A) to your current ERP system? Want to see the status of shipments, deliveries, and transports right in the customer order? No problem: State-of-the-art APIs make it easy to integrate seamlessly into your IT environment.

* To learn the Basic concepts of the M\&A platform see [Basic concepts](doc:basic-concepts-1) .
* If you want to see an example how you could integrate M\&A into your ERP system see [Example Project](doc:example-project).

## Playing around with the API

If you just want to play around with the API Methods of a Monitoring & Alerting Engine, you can use one of the following options.

## Readme.io

* Go to the [API Reference](https://transport-freight-management.docs.developers.aeb.com/reference/receiveorder) of this documentation and navigate to the *Monitoring & Alerting* section.
* Authenticate yourself by entering "*user*@*client*" and your password into the auth popup, right next to the *try it* button.

## Swagger

* Authenticate yourself by clicking the Authorize button at the top of the page.
* Go to the [Swagger of the demo engine](https://rz3.aeb.de/demo1ma/swagger/)
* Navigate to the LISBF20Bean section of the page for the M\&A methods.

## Manually setting up the API

The M\&A API methods can be found at: 

## REST (OpenApi)

`*ENGINE_URL*/rest/openapi.json` (e.g. `https://rz3.aeb.de/demo1ma/rest/openapi.json`)

## SOAP

`*ENGINE_URL*/servlet/bf/LISBF20?WSDL` (e.g. `https://rz3.aeb.de/demo1ma/servlet/bf/LISBF20?WSDL`)

For Authentication see: [REST Authentication](https://transport-freight-management.docs.developers.aeb.com/v2/docs/setup-your-environment-1#section-rest-authentication)
