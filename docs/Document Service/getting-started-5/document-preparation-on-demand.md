---
title: On-Demand Documents
excerpt: >-
  Documents are created on the per-request basis. No permanent document storage
  is provided. Document data must always be transmitted in the request in order
  to get a valid document. Each document creation is subject to a fee.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
## Try it out

When you have selected a &lt;&lt;glossary:Document template&gt;&gt; and prepared some suitable data that match the &lt;&lt;glossary:Document schema&gt;&gt; of the template, you can generate your first document.

Alternatively, you can just use the predefined example values for the `DemoDoc10.pdf`.

### Using Swagger UI

The most comfortable way is to use the [Swagger UI](https://rz3.aeb.de/demo1docs/swagger/#/DocumentService/createDocument_1):

- fill-in the `processor` and `templateName`
- select a `format` that is supported by the associated `processor`
- clear the staging parameters (`referenceNumber`, `referenceType`, `documentType` and `retentionDaysLimit`) – otherwise the document would be stored in the Document Service and this use-case is not covered in this chapter
- you can define the requested document file name in `documentName` (w/o the file extension)
- upload your example file to the `Request body`; ensure that the content type matches your data format (XML and JSON is supported)

Now execute the request

<div align="center">
  <img src="https://files.readme.io/95ca585-image.png" alt="" style={{ border: true }} />
</div>

You get a response like this:

<div align="center">
  <img src="https://files.readme.io/810c9e1-image.png" alt="" style={{ border: true }} />
</div>

You then use the _Download file_ link to save the response into a file on your computer.

### Using readme.io API Reference

The same request can be theoretically [executed here](/reference/createdocument_1), but there are the following problems:

- When your data example is in XML format, the request must contain this header: `Content-Type: application/xml`
- It is unclear how the body with the example data is actually uploaded (might use multipart form?)
- The generated PDF response is binary and it is hard to download/save it correctly

### Using command line

<div style={{ backgroundColor: "#018FF4", borderRadius: "5px", padding: "10px" }}>
  <span role="img" aria-label="keyboard">⌨️</span>
  <a href="https://transport-freight-management.docs.developers.aeb.com/v3/recipes/create-example-document" style={{ color: "white", textDecoration: "none" }}>
    <strong>Create Example Document</strong>
  </a>
</div>