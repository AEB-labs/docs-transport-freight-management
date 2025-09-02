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

When you have selected a <<glossary:Document template>> and prepared some suitable data that match the <<glossary:Document schema>> of the template, you can generate your first document.

Alternatively, you can just use the predefined example values for the `DemoDoc10.pdf`.

### Using Swagger UI

The most comfortable way is to use the [Swagger UI](https://rz3.aeb.de/demo1docs/swagger/#/DocumentService/createDocument_1):

- fill-in the `processor` and `templateName`
- select a `format` that is supported by the associated `processor`
- clear the staging parameters (`referenceNumber`, `referenceType`, `documentType` and `retentionDaysLimit`) – otherwise the document would be stored in the Document Service and this use-case is not covered in this chapter
- you can define the requested document file name in `documentName` (w/o the file extension)
- upload your example file to the `Request body`; ensure that the content type matches your data format (XML and JSON is supported)

Now execute the request

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/95ca585-image.png",
        null,
        ""
      ],
      "align": "center",
      "border": true
    }
  ]
}
[/block]

You get a response like this:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/810c9e1-image.png",
        null,
        ""
      ],
      "align": "center",
      "border": true
    }
  ]
}
[/block]

You then use the _Download file_ link to save the response into a file on your computer.

### Using readme.io API Reference

The same request can be theoretically [executed here](/reference/createdocument_1), but there are the following problems:

- When your data example is in XML format, the request must contain this header: `Content-Type: application/xml`
- It is unclear how the body with the example data is actually uploaded (might use multipart form?)
- The generated PDF response is binary and it is hard to download/save it correctly

### Using command line


[block:tutorial-tile]
{
  "backgroundColor": "#018FF4",
  "emoji": "⌨️",
  "id": "6426c42a3c4e4300183c0dd9",
  "link": "https://transport-freight-management.docs.developers.aeb.com/v3/recipes/create-example-document",
  "slug": "create-example-document",
  "title": "Create Example Document"
}
[/block]