---
title: updateDocument
excerpt: "<h3>Update an existing document or generate it in a different format either synchronously (wait for the result) or asynchronously (enqueue document creation and get the result later with the documentId).</h3> <p> Possibilities to update the stored document contents:<br /> <ul>   <li>`xml/json` data is filled + any of <b>Processing Options</b> is filled:<br />   \tThe contents of the document are completely replaced by newly created ones</li>   <li>`xml/json` data is <em>not</em> filled + any of <b>Processing Options</b> is filled:<br />   \tThe contents are created or updated using the existing document data stored together with the document.<br />   \tExisting contents are retained. For example, it allows to add content in a new format.</li>   <li>`xml/json` data is filled + none of <b>Processing Options</b> is filled:<br />   \tAll existing contents are recreated/updated with the new document data.</li> </ul> </p> If the stored document is archived a new revision will be created in the connected archive."
api:
  file: document-service-http-api.json
  operationId: updateDocument_1
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---