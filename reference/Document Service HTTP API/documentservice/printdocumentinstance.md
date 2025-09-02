---
title: printDocumentInstance
excerpt: >-
  <h3>Create a print request for document instance.</h3><p>Creates a print
  request for the requested document. The document must have been created by
  <code>POST
  /documentInstance/{referenceType}/{referenceNumber}/{documentType}</code> and
  defined by its documentId.The printing location depends on the session context
  (e.g. user/client or workstation) and the printing output settings in the
  document type of the document.</p><p>The print request is processed
  asynchronously and may fail if the cloud printing server service is not
  started on the target machine. When the print request is processed the
  <b>actual content</b> of the document will be printed, e.g. if the document
  has been changed since the print request was created the changes will be
  printed.</p>
api:
  file: document-service-http-api.json
  operationId: printDocumentInstance
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---