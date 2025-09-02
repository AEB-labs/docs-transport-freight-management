---
title: Reference Object Maintenance
excerpt: >-
  Reference objects are local representatives for your external business
  objects. These objects are uniquely identified by a reference type, e.g.
  Shipment, Package, Handling unit etc., and a free-form reference number. The
  reference types must be configured manually.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
# Search Reference Objects

The information on the existing reference objects for a specific <<glossary:Reference object type>> can be searched for and filtered by:

- Exact match for `referenceType` (required parameter)
- The sorting order by `referenceNumber` is available
- The number of records returned in the response is limited to max. 100. The total number of existing records can be returned, if `returnTotalCount` is set to `true` (by default is it switched off, to avoid an additional count-query). Result scrolling window (paging) can be achieved by setting `maxResult` (window/page size) and `skipFirst` (number of top records to ignore).

## Try it out

Use [reference objects query](/reference/querydocumentreferenceobjects) and fill-in the filter as desired.

You get a response like this:

```json
{
  "hasErrors": false,
  "hasOnlyRetryableErrors": false,
  "hasWarnings": false,
  "messages": [],
  "referenceObjects": [
    {
      "referenceType": {
        "code": "SHIPMENT",
        "label": "Shipment"
      },
      "referenceNumber": "4711",
      "documentInfos": [
        {
          "documentId": "defe7075-3318-49b9-91e5-788034dc8cdf",
          "description": "Example document",
          "createdAt": "2023-05-25T13:37:00",
          "createdUserName": "API_TEST"
        },
        {
          "documentId": "b8de1266-0711-4d26-a791-5249e9ab793c",
          "description": "DEMODOC",
          "createdAt": "2023-05-25T14:51:22",
          "createdUserName": "API_TEST"
        }
      ]
    }
  ]
}
```

There is also a list of `documentInfos` within each reference object, representing the existing documents. Note that only an **information** on the contained document is returned (meta-data). To retrieve the actual <<glossary:Document content>> of an individual document, a full combination of `referenceType`, `referenceNumber` and `documentType` (or a concrete `documentId` ) must be used in a separate request.

# Query one Reference Object

When you specify both  `referenceType` and `referenceNumber`, a single reference object is located.

## Try it out

Use [reference object query](/reference/getdocumentreferenceobject) and fill in the desired object identification.

You get a response like this:

```json
{
  "hasErrors": false,
  "hasOnlyRetryableErrors": false,
  "hasWarnings": false,
  "messages": [],
  "state": "SUCCESS",
  "referenceObject": {
    "referenceType": {
      "code": "SHIPMENT",
      "label": "Shipment"
    },
    "referenceNumber": "4711",
    "documentInfos": [
      {
        "documentId": "defe7075-3318-49b9-91e5-788034dc8cdf",
        "description": "Example document",
        "createdAt": "2023-05-25T13:37:00",
        "createdUserName": "API_TEST"
      },
      {
        "documentId": "b8de1266-0711-4d26-a791-5249e9ab793c",
        "description": "DEMODOC",
        "createdAt": "2023-05-25T14:51:22",
        "createdUserName": "API_TEST"
      }
    ]
  }
}
```

The response is similar to the search query from above, but contains just one `referenceObject` element. The response is `404` if the object didn't exist.

# Create or Update Reference Object

The _Reference objects_ can be automatically created upon document creation requests (see `autoCreateRefObject`). Alternatively, you can restrict the document creation only to existing reference objects and require their explicit creation.

If the specified reference object already exists, it is updated. As there is no other relevant data besides the `referenceType` and `referenceNumber`, the update is just a dummy operation that does nothing. However, that can change in future releases if the reference objects get some additional properties.

## Try it out

Use [update reference object](/reference/updatedocumentreferenceobject) request and fill-in the object identification as desired.

You get an empty `204` response.

# Remove Reference Object

If the business object representative is no more needed, it can be removed.

The contained documents will be discarded, too, unless it is explicitly requested to retain them (see the `preserveDocuments` parameter - the documents are then still accessible via the _Staged documents_ interface after the deletion of the reference object).

A good practice could be to bind the creation and deletion of the reference objects to the lifecycle of the original business object in the host system.

## Try it out

Use [delete reference object](/reference/deletedocumentreferenceobject) request and fill-in the object identification as desired.

You get an empty `204` response (or `404` if the object didn't exist).

If you now [query](/reference/getdocumentreferenceobject) the reference object, it is no more there.