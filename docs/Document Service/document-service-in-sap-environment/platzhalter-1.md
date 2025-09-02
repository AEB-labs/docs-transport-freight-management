---
title: Setting up your SAP environment (Document Service)
excerpt: This documentation describes how to use the Document Service from SAP via REST
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: platzhalter2
      title: Creation of the first document
---
## Credentials

Before you can start using the Document Service API, you need a client, a user and a password.\
For testing you can use:\
[https://rz3.aeb.de/demo1docs/](https://rz3.aeb.de/demo1docs/)\
Mandant(client): APITEST\
User: API\_TEST\
PW: API\_TEST2021

## Set up the connection in SM59

First you must create a new connection type G in SM59.

Host: rz3.aeb.de

Port: 443

Path prefix: /*test1docs*/rest/DocumentService/document (this may be different depending on which instance your client runs)

![](https://files.readme.io/d11bce1636b559f6df011139bd0b7a6268c7f3b214a99ca34f1089f28db166dd-image.png)

In Logon & Security you  enter the credentials in the pattern user\@client with the required password and active the SSL client standard store.

![](https://files.readme.io/fe1b2901666d5a9728af8619ba33e2653a5d7c19d8d5c79fcbe293d2cd5615f2-image.png)

<br />

## Import certificates to STRUST

To enable a direct HTTPS connection between the SAP system and the AEB data center, you need to import the necessary SSL certificates. Please refer to this documentation how to do: [https://rz3.aeb.de/docudata/inst-config-guides/customs-management/installconfig-customsmgmt-plug-insap/en-US/index.html#384034443391691019](https://rz3.aeb.de/docudata/inst-config-guides/customs-management/installconfig-customsmgmt-plug-insap/en-US/index.html#384034443391691019)

## Additional connection for Application facade

If you want to use the application facade of the Document Service (e.g. for the type write mode) you will have to set up a second connection with a different path prefix /*test1docs*/rest/DocumentService/ui/document  (this may be different depending on which instance your client runs).
