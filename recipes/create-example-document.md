---
title: Create Example Document
description: Prepare an example PDF document from the command line (using curl on Windows)
hidden: false
recipe:
  color: '#018FF4'
  icon: ⌨️
---
```shell curl (Windows)
curl --user API_TEST@APITEST:API_TEST2021 --output DemoDoc10.example.xml --get "https://rz3.aeb.de/demo1docs/rest/DocumentService/template/DemoDoc10.pdf/parse?processor=PDF-XFA&query=XML%3FDemoDoc10.example.xml"
type DemoDoc10.example.xml
curl --user API_TEST@APITEST:API_TEST2021 --header "Content-Type: application/xml" --data-binary "@DemoDoc10.example.xml" --output DemoDoc10.example.pdf "https://rz3.aeb.de/demo1docs/rest/DocumentService/document?async=false&processor=PDF-XFA&templateName=DemoDoc10.pdf&format=PDF&documentName=DemoDoc10Example"
DemoDoc10.example.pdf

```

```json Response Example
curl 7.83.1 (Windows) libcurl/7.83.1 Schannel
Release-Date: 2022-05-13
```

# Download example data

<!-- shell@1 -->

Download example XML data and save it to local file "DemoDoc10.example.xml"

# Check returned data

<!-- shell@2 -->

The file DemoDoc10.example.xml must exists and contain valid XML data.

# Create example document

<!-- shell@3 -->

Prepare a document using the downloaded data and save it to local file "DemoDoc10.example.pdf"

# Open created document

<!-- shell@4 -->

Open the generated PDF document in your local application