---
title: createDocumentInstance
excerpt: >-
  <h3>Generate a new document instance.</h3><p>Prepares a document immediately
  within response or asynchronously from the referenced document type and
  document data. The document type and reference object are resolved in the
  context of the session client. The output format and archive options are
  defined in the referenced document type. Created documents are retained for
  later reuse, e.g. fetching or printing the document. The caller can fetch the
  document contents by calling <code>GET /document/{documentId}</code> with the
  received documentId or <code>GET
  /documentInstance/{referenceType}/{referenceNumber}/{documentType}</code>. An
  existing document can be updated by specifying the reference object and stored
  as a new revision in the archive if it has to be or was previously
  archived.</p>
api:
  file: document-service-http-api.json
  operationId: createDocumentInstance
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---