---
title: Create and Edit Staged Document
description: >-
  Prepare an example PDF document asynchronously and edit its data in a WYSIWYG
  application, using the command line (curl on Windows)
hidden: false
recipe:
  color: '#018FF4'
  icon: ⌨️
---
```shell curl (Windows)
curl --user API_TEST@APITEST:API_TEST2021 --output DemoDoc10.example.xml --get "https://rz3.aeb.de/demo1docs/rest/DocumentService/template/DemoDoc10.pdf/parse?processor=PDF-XFA&query=XML%3FDemoDoc10.example.xml"
curl --user API_TEST@APITEST:API_TEST2021 --header "Content-Type: application/xml" --data-binary "@DemoDoc10.example.xml" --dump-header DemoDoc10.example.hdr "https://rz3.aeb.de/demo1docs/rest/DocumentService/document?async=true&processor=PDF-XFA&templateName=DemoDoc10.pdf&format=PDF&documentName=DemoDoc10Example&referenceNumber=4711&referenceType=SHIPMENT&documentType=DEMODOC&retentionDaysLimit=3"
for /f "tokens=2 delims=<>" %l in ('findstr /R "link: <[a-zA-Z0-9/-]+>"  DemoDoc10.example.hdr') do set DemoDoc10.example.link=%l
echo Document creation requested: %DemoDoc10.example.link%
echo Wait a while until the document is ready, then continue to edit & ping -n 3 -w 1000 localhost >nul
set DemoDoc10.editorAction=EDIT
start https://API_TEST%40APITEST:API_TEST2021@rz3.aeb.de/demo1docs/rest/DocumentService/ui/%DemoDoc10.example.link%?editorAction=%DemoDoc10.editorAction%^&user=DemoUser^&redirect=true
rem Don't forget to CLOSE the application, otherwise the document stays LOCKED
```

```json Response Example
curl 7.83.1 (Windows) libcurl/7.83.1 Schannel
Release-Date: 2022-05-13
```

# Download example data

<!-- shell@1 -->

Download example XML data and save it to local file "DemoDoc10.example.xml"

# Request example document creation

<!-- shell@2 -->

Request an asynchronous preparation of a document using the downloaded data. The document id/link is to be found in the response or in the local file "DemoDoc10.example.hdr".

# Extract the document id

<!-- shell@3-4 -->

Extract the returned document id/link for later use. The result is stored in the local variable "DemoDoc10.example.link".

# Wait for the document

<!-- shell@5 -->

It can take some time until the document is ready. You can use the previously returned document id/link to check its state periodically or on demand. Confirm when you are ready to continue.

# Open document for editing

<!-- shell@6-8 -->

Invoke a UI session URL that allows you to manually edit and save the document's data in a nearly WYSIWYG application. The document content is then regenerated with the changed data.
Tip: try out to set editorAction=PREVIEW