---
title: Staged Document Instances
excerpt: >-
  The term "Instance" is used to stress out that the staged documents strictly
  reference predefined document types and reference object instances. Manual
  configuration of the document types and reference object types is required.
  Staged document instances support advanced archiving configuration and direct
  document printing. Each reference object then knows all its document types and
  offers the document instances for them.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Data Model

Contrary to the plain staged documents, the document instances require that all the staging parameters are filled and refer to a valid <Glossary>Reference object type</Glossary> and <Glossary>Document type</Glossary> (the *Reference object* can be automatically created on demand).

<Image alt="Staged Document Instances Model" align="center" src="https://files.readme.io/0953d70-image.png">
  Staged Document Instances Model ([https://online.visual-paradigm.com/](https://online.visual-paradigm.com/))
</Image>

<Callout icon="📕" theme="default">
  ### There is a *restriction on uniqueness* of `referenceType`, `referenceNumber` and `documentType`, i.e. each *Document type* can be used only once within a single *Reference Object* instance. However, it *is* possible to use one <Glossary>Document template</Glossary> in several *Document types*.
</Callout>

<Callout icon="📒" theme="default">
  ### This restriction causes problems in certain situations, e.g. when free-floating documents (w/o any "owner") should be created or an unknown number of unidentified external documents are to be attached to a single object. We will try to offer an improved solution in the future.
</Callout>

<Callout icon="📒" theme="default">
  ### You shouldn't mix together the *Staged Document Instances* and plain *Staged Documents* using the same combination of `referenceType`, `referenceNumber` and `documentType`. Although such usage is not restricted, it can lead to unexpected results when you search for or use the documents.
</Callout>

## Using Reference objects

Contrary to the [Staged Documents](doc:document-preparation-staged), the central entity in this model is not the document itself, but the *Reference object* instance, as a representative of your external business entity. A document then *belongs* to such a representative.

An other difference is that the configured <Glossary>Document type</Glossary>s replace a simple <Glossary>Document template</Glossary> reference. A new template can then simply replace an old one in the configuration without changing the document type name.

This is the identical data model which is used in some other AEB products that work with documents. The main difference compared to the *Document Service* is that the individual products already *posses* concrete business objects, like Shipment, Package, Handling unit etc. together with their corresponding business data, whereas the *Document Service* only mimics these objects by a generic *Reference object* and the data must be passed from outside in the individual document requests.

# Example Configuration Data

We have already prepared a **SHIPMENT** reference type and two document types that are attached to it:

* **DEMODOC**, used to generated PDF documents from the *DemoDoc10.pdf* template
* **INVOICE**, used to be associated with an externally uploaded document

These two documents can be created for any SHIPMENT reference object (e.g. SHIPMENT 4711, SHIPMENT 4712 etc).

# Document Preparation

When you have selected a <Glossary>Document type</Glossary> and prepared some suitable data that match the <Glossary>Document schema</Glossary> associated with the referenced template, you can generate your document.

Alternatively, you can just use the **DEMODOC** document type and a predefined example values for the `DemoDoc10.pdf`.

Each document instance is identified by a unique combination of `referenceType`, `referenceNumber` (which identify the associated *Reference object*) and `documentType` (which identifies the associated *Document type*). This combination can be used to

* fetch previously generated document
* update/overwrite an existing document with a new content

All document contents are created that are needed for printing, preview and archiving. The required formats are configurable in the *Output settings* of the  *Document type*.

## Try it out

The most comfortable way is to use the [Swagger UI](https://rz3.aeb.de/demo1docs/swagger/#/DocumentService/createDocumentInstance). It works basically the same way as for the [Staged Documents](doc:document-preparation-staged), only the staging parameters are required and their combination uniquely identifies a document instance.

* fill-in the required parameters (`referenceType`, `referenceNumber`, `documentType`); the referenced <Glossary>Reference object type</Glossary> and <Glossary>Document type</Glossary> must already had been configured
* ensure that `autoCreateRefObject` is set to **true** (otherwise you'd need to create the required reference object [explicitly](doc:reference-object-maintenance))
* upload your example file to the `Request body`; ensure that the content type matches your data format (XML and JSON is supported)

The request can now be executed either *synchronously* (you get the prepared document in the response) or *asynchronously* (you can [ask for the document later](https://rz3.aeb.de/demo1docs/swagger/#/DocumentService/getDocumentInstance)).

Similarly you can [upload an external document](https://rz3.aeb.de/demo1docs/swagger/#/DocumentService/updateDocumentInstance). The referenced document type must be configured with the *Program/format* "External document" (<Glossary>Document processor tag</Glossary> EXTPRINTABLE).

# Download Document Contents

Identified by `referenceType`, `referenceNumber`, `documentType`, an actual <Glossary>Document content</Glossary> can be downloaded from the *Reference object*.

If the document contains several contents, the `contentVariant` can be used to specify the required one.

## Try it out

The most comfortable way is to use the [Swagger UI](https://rz3.aeb.de/demo1docs/swagger/#/DocumentService/getDocumentInstance). Fill-in the required reference fields (and, if applicable, also the `contentVariant`) and execute the request.

Use the *Download file* link to save the content to a file on your computer.

Alternatively, using a direct `documentId` reference can [still be used](https://rz3.aeb.de/demo1docs/swagger/#/DocumentService/getDocument), too.

# Available and Created Documents of a Reference Object

In the context of an <Glossary>Reference object type</Glossary>, identified by a `referenceType` and `referenceNumber`, the following document information is available:

* Configured, but **not yet existing** documents of a <Glossary>Document type</Glossary>
* Configured and **existing** documents of a <Glossary>Document type</Glossary>
* Document **attachments** without any <Glossary>Document type</Glossary> configuration (plain *Staged Documents* created with matching `referenceType` and `referenceNumber`). The individual attached documents are identifiable via its `documentId` only. Note that if a <Glossary>Document type</Glossary> configuration is removed or renamed, the corresponding existing documents are effectively turned into such attachments.

Note that only an **information** on the staged documents is returned (meta-data). To retrieve the actual <Glossary>Document content</Glossary> of an individual document, a unique combination of `referenceType` and `referenceNumber` and `documentType` (or a distinct `documentId`) must be used in a separate request.

Note that the actual document contents might have already expired and is no more available (it is preserved for at most 90 days). The document meta-data are kept for 18 months.

## Try it out

Use [document instance query](/reference/getdocumentinstances) and fill-in the `referenceType` and `referenceNumber` as desired.

You get a response like this:

```json
{
  "hasErrors": false,
  "hasOnlyRetryableErrors": false,
  "hasWarnings": false,
  "messages": [],
  "state": "SUCCESS",
  "documentInfos": [
    {
      "documentInstanceReference": {
        "documentTypeRef": {
          "identCode": "INVOICE"
        },
        "documentReferenceObjectRef": {
          "referenceType": "SHIPMENT",
          "referenceNumber": "4711"
        }
      }
    },
    {
      "documentId": "1bebab3f-f7d3-4815-b299-4d213d7e81aa",
      "documentReference": {
        "documentType": "DEMODOC",
        "referenceType": "SHIPMENT",
        "referenceNumber": "4711"
      },
      "description": "Example document",
      "createdAt": "2023-09-09T09:46:17",
      "createdUserName": "API_TEST",
      "archivedState": "NONE",
      "retentionTimestamp": "2023-09-12T09:46:17",
      "documentContentStoreInfos": [
        {
          "name": "DemoDoc10_PDF",
          "mimeType": "application/pdf",
          "contentVariant": "PDF"
        },
        {
          "name": "DemoDoc10_PDFA",
          "mimeType": "application/pdf",
          "contentVariant": "PDFA"
        }
      ],
      "documentInstanceReference": {
        "documentTypeRef": {
          "identCode": "DEMODOC"
        },
        "documentReferenceObjectRef": {
          "referenceType": "SHIPMENT",
          "referenceNumber": "4711"
        }
      }
    },
    {
      "documentId": "d286b360-1082-42aa-84eb-9f801114205b",
      "documentReference": {
        "documentType": "attachment",
        "referenceType": "SHIPMENT",
        "referenceNumber": "4711"
      },
      "description": "attachment",
      "createdAt": "2023-09-09T11:36:26",
      "createdUserName": "API_TEST",
      "archivedState": "NONE",
      "retentionTimestamp": "2023-09-12T11:36:26",
      "documentContentStoreInfos": [
        {
          "name": "info",
          "mimeType": "application/pdf"
        }
      ],
      "documentInstanceReference": {
        "documentReferenceObjectRef": {
          "referenceType": "SHIPMENT",
          "referenceNumber": "4711"
        }
      }
    }
  ]
}
```

* The first entry is a **not yet existing** document for the configured `INVOICE` <Glossary>Document type</Glossary>.
* The second entry is a created, **existing** document for the configured `DEMODOC` <Glossary>Document type</Glossary>. It has two contents (variants/formats "PDF" and "PDFA").
* The third entry is an **attached** document "info.pdf" without any <Glossary>Document type</Glossary> configuration. **Note** that the `documentTypeRef` entry in the `documentInstanceReference` element is **missing** in this case.
