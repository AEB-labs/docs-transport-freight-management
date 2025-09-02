---
title: createDocument
excerpt: >-
  <h3>Generate a new document either synchronously (wait for the result) or
  asynchronously (enqueue document creation and get the result later with the
  provided documentId).</h3><p>Creates a document from the referenced template
  and document data. The template is resolved in the context of the session
  client. If any of the <b>Staging options</b> is filled the created document
  contents will be retained for later reuse.<br/>An existing document can be
  updated in `POST /document/{documentId}` and stored as a new revision in the
  archive in case it was previously archived.<br/>The update can be done in
  different ways, see the description for `POST /document/{documentId}`
api:
  file: document-service-http-api.json
  operationId: createDocument_1
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---