---
title: updateDocumentInstance
excerpt: >-
  <h3>Update specified document instance.</h3><p>Uploads an external document
  which does not depend on templates of the document. The document type and
  reference object are resolved in the context of the session client. The
  archive options are defined in the referenced document type. Like <code>POST
  /documentInstance/{referenceType}/{referenceNumber}/{documentType}</code> the
  uploaded document can be queried, deleted and fetched by calling the
  corresponding method with the received documentId.The document also has a date
  to which this document is at least stored in the document store.<br/>Currently
  only PDF up to a maximum size of 10MB is supported.</p>
api:
  file: document-service-http-api.json
  operationId: updateDocumentInstance
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---