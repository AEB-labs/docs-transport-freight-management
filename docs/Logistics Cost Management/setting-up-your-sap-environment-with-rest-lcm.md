---
title: Integrate your SAP system using REST
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: creating-data-classes
      title: Creating data classes
---
The advantage of using the REST API is you don't have to import the WSDL into SAP and you don't need any proxy class or logical port. First thing we still need though is a connection type G you can set up via transaction SM59. 

- Host: rz3.aeb.de
- Port: 443
- Path Prefix: /test2billing/rest/BillingBFBean (you will get the final endpoints for test and production from your AEB consultant or from the AEB portal)
- User and password will be provided to you from AEB
- SSL needs to be active and the certificate store is DEFAULT SSL Client (Standard)

![](https://files.readme.io/4a489a90dc28a4ecf11456d10fe184e1514bc317d1ef1c72e4b44c31cc63190f-image.png)

![](https://files.readme.io/468c2524045b385bb6d2e10d87cf9988ee879d69184add396364b34b3707c0b5-image.png)

<br />

This configuration will enable you to access all methods from <https://rz3.aeb.de/test2billing/swagger/#/Billing>.

For the connection to work you need to import the SSL certificates from AEB like described in this documentation: <https://rz3.aeb.de/docudata/inst-config-guides/carrier-connect/installconfig-carrierconnect-plug-insap/en-US/index.html#384034443665524875>.