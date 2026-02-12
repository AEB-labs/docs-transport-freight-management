---
title: createDocument
excerpt: >-
  <h3>Upload an external document</h3><p>Uploads an external document (which
  does not depend on any document templates). Like `POST /document`, the
  uploaded document can be queried, deleted and fetched by calling the
  corresponding method with the received `documentId`. The document also has a
  date to which it is at least stored in the document store.<br/>Currently only
  PDF documents up to a maximum size of 10MB are supported, without embedded
  links, scripts or attachments.</p>
api:
  file: document-service-http-api.json
  operationId: createDocument
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---