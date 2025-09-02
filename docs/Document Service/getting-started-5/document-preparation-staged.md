---
title: Staged Documents
excerpt: >-
  Documents are created synchronously or asynchronously and a document storage
  is provided for a limited time. Documents can be tagged with a reference to a
  related business object and/or document type. Only the first creation of the
  document creation is subject to a fee. Document updates or creation of
  additional document contents are free of charge.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Synchronous and Asynchronous Document Preparation

When you have selected a <<glossary:Document template>> and prepared some suitable data that match the <<glossary:Document schema>> associated with the template, you can generate your document.

Alternatively, you can just use the predefined example values for the `DemoDoc10.pdf`.

Each staged document is identified by unique `documentId`. The `documentId` can be used to

- fetch a previously generated document
- update/overwrite an existing document with a new content
- generate additional contents for an existing document, using the original data

## Try it out

### Using Swagger UI

The most comfortable way is to use the [Swagger UI](https://rz3.aeb.de/demo1docs/swagger/#/DocumentService/createDocument_1). It works basically the same way as for the [On-Demand Documents](doc:document-preparation-on-demand), only some staging parameters need to be provided in the request.

- fill-in the `processor` and `templateName`
- select a `format` that is supported by the associated `processor`
- fill-in all or some of the staging parameters (`referenceNumber`, `referenceType`, `documentType` and `retentionDaysLimit`) – the document will be stored in the _Document Service_ for the required number of days (max. 90) for later reuse; a unique `documentId` will be generated for the document
- optionally, the document can be accompanied by a list of customized _tags_
- upload your example file to the `Request body`; ensure that the content type matches your data format (XML and JSON is supported)

The request can now be executed either _synchronously_ (you get the prepared document and the generated `documentId` in the response) or _asynchronously_ (your get only a generated `documentId` in the - otherwise empty - response and ask for the document later). The behavior is controlled by the `async` parameter (it is the first one). The asynchronous execution can be beneficial for situations when you have large documents and do not want to block your call request.

- Synchronous execution: ensure that the `async` parameter is set to `false`
- Asynchronous execution: ensure that the `async` parameter is set to `true`

Now execute the request

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d9efc3f-image.png",
        null,
        ""
      ],
      "align": "center",
      "border": true
    }
  ]
}
[/block]


In the response, you find the generated `documentId` in the `link` header (already embedded in the full relative request path to query the document):

![](https://files.readme.io/fb0d647-image.png)

### Using readme.io API Reference

The same request can be theoretically [executed here](/reference/createdocument_1), but there are the following problems:

- When your data example is in XML format, the request must contain this header: `Content-Type: application/xml`
- It is unclear how the body with the example data is actually uploaded (might use multipart form?)
- The generated PDF response is binary and it is hard to download/save it correctly
- The `link` header (with the `documentId`) is not displayed in the response

# Upload External Documents

The _Document Service_ also offers you the option of storing PDF documents and forms that were not created _via_ the _Document Service_.

- Currently, only PDF documents and forms that are intended for printing or previewing are allowed to be uploaded. During the upload, the system checks whether the document or form is actually a PDF document or form (the extension .pdf is not sufficient).
- The external PDF documents/forms do not allow the use of password prompts, attachments,  
  scripts and shell statements, forms such as AcroForms® or XFA, and hyperlinks. Such documents will result in the  
  rejection of the upload.
- You can upload external documents/forms up to a maximum size of 10 MB per document/form.  
  In case of larger documents, it is necessary to split them in advance if you can't reduce the size otherwise.

## Try it out

### Using Swagger UI

The most comfortable way is to use the [Swagger UI](https://rz3.aeb.de/demo1docs/swagger/#/DocumentService/createDocument).

- fill-in the intended `fileName` (inclusive the file extension)
- fill-in all or some of the staging parameters as described above
- upload your example file to the `Request body`

Now execute the request. You get the `documentId` in the `link` header again, as described above.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ec08270-image.png",
        null,
        ""
      ],
      "align": "center",
      "border": true
    }
  ]
}
[/block]


### Using readme.io API Reference

Theoretically you can [upload here](/reference/createdocument) the document, but there are the following problems:

- The request must contain this header: `Content-Type: application/pdf`
- The PDF content must be contained directly in the request body payload