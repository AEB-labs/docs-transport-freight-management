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
Want to manage your loading ramps efficiently? Want to have the overview when your loading ramps are used? Want to connect AEB Loading Dock Scheduling (LDS) to your current ERP system? No problem: State-of-the-art APIs make it easy to integrate seamlessly into your IT environment.

## Playing around with the API

If you just want to play around with the API Methods of a Loading Dock Scheduling Engine, you can use one of the following options.

## Readme.io

* Go to the [API Reference](https://transport-freight-management.docs.developers.aeb.com/reference/createloadingorder) of this documentation and navigate to the *Loading Dock Scheduling* section.
* Authenticate yourself by entering "*user*@*client*" and your password into the auth popup, right next to the *try it* button.

## Swagger

* Authenticate yourself by clicking the Authorize button at the top of the page.
* Go to the [Swagger of the demo engine](https://rz3.aeb.de/demo1ma/swagger/)
* Navigate to the TSMBFBean section of the page for the LDS methods.

## Manually setting up the API

The LDS API methods can be found at: 

## REST (OpenApi)

`*ENGINE_URL*/rest/openapi.json` (e.g. `https://rz3.aeb.de/demo1ma/rest/openapi.json`)

## SOAP

`*ENGINE_URL*/servlet/bf/TSMBF?WSDL` (e.g. `https://rz3.aeb.de/demo1ma/servlet/bf/TSMBF?WSDL`)

For Authentication see: [REST Authentication](https://transport-freight-management.docs.developers.aeb.com/v2/docs/setup-your-environment-1#section-rest-authentication)
