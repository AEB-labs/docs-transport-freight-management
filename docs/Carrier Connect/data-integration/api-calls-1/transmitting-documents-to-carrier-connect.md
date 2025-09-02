---
title: Attach and upload documents to transmit them to the carrier
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

At times, it becomes necessary to electronically transmit documents, such as export accompanying documents, to a carrier. Our [addShipmentAttachments](https://transport-freight-management.docs.developers.aeb.com/reference/addshipmentattachments) API call offers a convenient solution for attaching documents to an existing shipping order. Alternatively, you can manually attach a document via the Carrier Connect GUI. 

For electronic transmission of documents to a carrier, it is imperative to have an appropriate value-added service, such as "DHL Express Paperless Trade", implemented in Carrier Connect. By selecting this service in the shipping order, you can seamlessly transmit the required documents to the carrier. For further details, please refer to our <a href="https://docs.aeb.com/doc/cm-408620299-881238923-en-US/t-881238923-408620299-en-US" target="_blank">system description</a>.

<Callout icon="💡" theme="default">
  ### How to transmit documents manually

  Learn how to manually transmit documents electronically to carriers via Carrier Connect: <a href="https://docs.aeb.com/doc/cm-620065803-801708043-en-US/t-801708043-795475083-en-US" target="_blank">Document upload</a>
</Callout>

```json
{
  "clientSystemId": "ERP",
  "clientIdentCode": "APITEST",
  "userName": "API_TEST",
  "resultLanguageIsoCodes": "en",
  "shipmentReference": {
    "shipmentNumber": "SHIPMENT_TEST_1"
  },
  "mode": "UPDATE",
  "attachments": [
    {
      "filename": "invoice.pdf",
      "mimeType": "application/pdf",
      "data": "Put your base64 encoded document content here",
      "contentType": "PRO_FORMA_INVOICE"
    }
  ]
}

```
```xml
  <clientSystemId>ERP</clientSystemId>
  <clientIdentCode>APITEST</clientIdentCode>
  <userName>API_TEST</userName>
  <resultLanguageIsoCodes>en</resultLanguageIsoCodes>
  <shipmentReference>
    <shipmentNumber>SHIPMENT_TEST_1</shipmentNumber>
  </shipmentReference>
  <mode>UPDATE</mode>
  <attachments>
    <filename>invoice.pdf</filename>
    <mimeType>application/pdf</mimeType>
    <data>akfasjfkasdjlfakHH</data>
    <contentType>PRO_FORMA_INVOICE</contentType>
  </attachments>
```

## Things to Keep in Mind

* When you attach a document please ensure that the relevant shipping order is not marked as completed (`doCompletion = false`).
* You must base64 encode the document content and put it in `attachments > data`.
