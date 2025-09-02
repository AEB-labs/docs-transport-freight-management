---
title: User Interface
excerpt: >-
  There are several situations where manual interaction via user interface is
  needed. The access to some basic applications can be obtained in form of a
  pre-authenticated URL from specialized "ui" API.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
> 📘 Any application is opened in a statefull session, do not forget to _close_ it when you are finished with your work.

# Document Overview

For manual interactive document maintenance, use [UI/Application Facade](/reference/openstageddocumentsearch) to get a short-live, pre-authenticated URL link to the [Document Search Application](https://API_TEST%40APITEST:API_TEST2021@rz3.aeb.de/demo1docs/rest/DocumentService/ui/document?user=DemoUser&language=en&redirect=true):

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/664c4a1-image.png",
        null,
        ""
      ],
      "align": "center",
      "border": true
    }
  ]
}
[/block]


This application allows you to

- filter existing documents by various criteria
- show or download contents of individual documents
- display properties of individual documents (when it was created etc.)
- delete documents

## Try it out

### Redirected Request

Open the [Document Search Application](https://API_TEST%40APITEST:API_TEST2021@rz3.aeb.de/demo1docs/rest/DocumentService/ui/document?user=DemoUser&language=en&redirect=true) directly. The authentication is already included in the URL and a  `303 SEE OTHER` redirection result is generated. The request is based on [ui/openStagedDocumentSearch](/reference/openstageddocumentsearch) with `redirect=true`.

This technique is designed to be used:

- for presentation purposes in a browser (the browser resolves the redirection, like in the link above)
- when the 303 response is resolved explicitly in your code (the target URL must be extracted for the `Location` header)

### Regular Response

Fill in the required user, language and filter parameters in [ui/openStagedDocumentSearch](/reference/openstageddocumentsearch). Ensure that `redirect` is **not** set. Then execute the request.

You get a `200` response like this (the format depends on the request `Accept` header):

```json
{
  "sessionid": "AFCall-Invoke12345",
  "httpUrl": "https://rz3.aeb.de/demo1docs/servlet/...",
  "urlCloseToken": "goodbypage"
}
```
```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
  <ApplicationFacade>
    <httpUrl>https://rz3.aeb.de/demo1docs/servlet/...</httpUrl>
    <sessionid>AFCall-Invoke12345</sessionid>
    <urlCloseToken>goodbypage</urlCloseToken>
  </ApplicationFacade>
```

To open the application, copy the value of the returned `httpUrl` and paste it into your browser (or into the Win+R Run command prompter). Alternatively, the URL can be extracted from the `link` header.

> 📘 The returned URL link is valid for a short period only (30 seconds).

This technique is designed to be used within code that prefers to handle `200` responses with access to either its payload data (JSON or XML) or headers.

### Internet Shortcut Download

Fill in the required user, language and filter parameters in [Swagger UI](https://rz3.aeb.de/demo1docs/swagger/#/DocumentService/openStagedDocumentSearch). Ensure that `redirect` is **not** set and select `application/internet-shortcut` for the response media type. Then execute the request.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/16f94b9-image.png",
        null,
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


You get a response like this:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7e8b511-image.png",
        null,
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


You then use the _Download file_ link to save the response into a shortcut-file on your computer. Then open the downloaded file and the application opens in your browser. You can also copy the application URL from the `link` header.

> 📘 The returned URL link is valid for a short period only (30 seconds). The downloaded file must be opened quickly.

Remark: The shortcut-file is a Windows format and the content looks like this:

```
[InternetShortcut]
URL=https://rz3.aeb.de/demo1docs/demo1docs_node1/servlet/...
```

This technique is designed to be easily used with Swagger UI.

# Print Request Overview

For manual interactive print request maintenance, use [UI/Application Facade](/reference/openprintrequestqueue) to get a short-live, pre-authenticated URL link to the [Print Queue Application](https://API_TEST%40APITEST:API_TEST2021@rz3.aeb.de/demo1docs/rest/DocumentService/ui/printQueue?user=DemoUser&language=en&redirect=true):

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c224dee-image.png",
        null,
        ""
      ],
      "align": "center",
      "border": true
    }
  ]
}
[/block]


This application allows you to

- see your pending print requests (optionally, printed requests can be displayed, too)
- restart, ignore or remove a failed print request
- remove pending requests

The print queue is by default bound to the authenticated user. Alternatively, a `workstationId` can be specified.

## Try it out

See the examples for _Document Overview_ above - the same techniques apply here, too.

# Document Editor

To manually preview a previously generated document or edit its data in a WYSIWYG editor, use  [UI/Application Facade](/reference/parsedocumenttemplatecontent) to get a short-live, pre-authenticated URL link to the application.

You need a valid `documentId` of the document.

## Try it out

### Using Swagger UI

Fill in the required user, language and `documentId` in  [Swagger UI](https://rz3.aeb.de/demo1docs/swagger/#/DocumentService/openStagedDocumentEditor). The default action is **PREVIEW**; set `editorAction` to **EDIT** if you want to enter the editor directly. Ensure that `redirect` is **not** set and select  `application/internet-shortcut` for the response media type. Then execute the request, follow the _Download file_ link and open the downloaded file.

You get something like this in your browser and you can edit and save the data there:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/399879b-image.png",
        null,
        ""
      ],
      "align": "center",
      "border": true
    }
  ]
}
[/block]


> 📒 The document is _exclusively locked_ as long as this application is open. It protects other users and background processes to interfere with your changes. It is _crucial_ that you close the editor when you are finished (either save or cancel). This editor is _not_ intended to preview the documents (use the document overview instead and open the document there).

### Using command line

[block:tutorial-tile]
{
  "backgroundColor": "#018FF4",
  "emoji": "⌨️",
  "id": "649ad40c78e725000cf65b0a",
  "link": "https://transport-freight-management.docs.developers.aeb.com/v3/recipes/create-and-edit-document",
  "slug": "create-and-edit-document",
  "title": "Create and Edit Document"
}
[/block]