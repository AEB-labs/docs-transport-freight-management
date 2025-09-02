---
title: Getting Started
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
You want to add document or label generation to your current ERP system? You want to print documents, or labels using data of your system? Or you need to upload, save and archive documents? Or do you intend to relate uploaded documents to a business object? No problem: State-of-the-art APIs make it easy to integrate document service into your IT environment.

# Tutorial

In order to optimally use the full potential of the _Document Service_, it is important to look around and see what's available there.

1. First, there are some [`<glossary:Document processor>`s](doc:document-processors). This helps you to understand what kind of documents we can generate for you.
2. Categorized by the `<glossary:Document processor tag>`, there exist `<glossary:Document template>`s. See which templates we have already [prepared for you](doc:document-templates).
3. Then, pick a template and [generate documents](doc:document-preparation) with it. Use the existing examples or your own data.

# Quick Examples

<TutorialTile
  backgroundColor="#018FF4"
  emoji="⌨️"
  link="https://transport-freight-management.docs.developers.aeb.com/v3/recipes/create-example-document"
  slug="create-example-document"
  title="Create Example Document"
/>

<TutorialTile
  backgroundColor="#018FF4"
  emoji="⌨️"
  link="https://transport-freight-management.docs.developers.aeb.com/v3/recipes/create-and-edit-staged-document"
  slug="create-and-edit-staged-document"
  title="Create and Edit Staged Document"
/>


# Playing around with the API

## Readme.io

- Go to the [API Reference](https://transport-freight-management.docs.developers.aeb.com/reference/querydocuments) of this documentation.
- Authenticate yourself by entering "_user_@_client_" and your password into the auth popup, right next to the _try it_ button.

## Swagger

- Go to the [Swagger UI of the demo engine](https://rz3.aeb.de/demo1docs/swagger/).
- Authenticate yourself by clicking the _Authorize_ button at the top of the page and entering your authentication data.
- Navigate to the [Document Service](https://rz3.aeb.de/demo1docs/swagger/#/DocumentService) section below on the page for the Document Service methods.

# Authentication data

User: API_TEST@APITEST (it is a combination of the internal User: API_TEST and Client: APITEST)  
Password: API_TEST2021

The API is only available via Secure Socket Layer (SSL).

# Response handling

## HTTP Status

Successfully processed requests usually return HTTP status code `200` (OK) or `202` (Accepted) or `204` (No Content). The following table contains an overview of generally used response codes.

| Code | Description          | Meaning                                                                                                                                                                                             |
| :--- | :------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 200  | OK                   | Request has been processed successfully and some data has been returned in the response.                                                                                                            |
| 202  | Accepted             | Request has been accepted for asynchronous processing. No data is returned yet, the caller is expected to poll the data in subsequent requests.                                                     |
| 204  | No Content           | Request has been processed successfully and no data is returned (e.g. deletion).                                                                                                                    |
| 300  | Multiple Choices     | Request has been accepted but the provided parameter are ambiguous. The request can be repeated with more specific values.                                                                          |
| 400  | Bad Request          | Request has been accepted but it contains invalid data or query-parameters. The request can be repeated with the correct values.                                                                    |
| 401  | Unauthorized         | Authorization header is missing, You must provide your authentication data within each request.                                                                                                     |
| 403  | Forbidden            | Authorization was provided but the access to the function has been denied. Let the administrator to check your authentication data and assigned roles.                                              |
| 404  | Not Found            | Request has been accepted but there is no object that corresponds to the specified identifier (required path-parameters).                                                                           |
| 410  | Gone                 | Request has been accepted but the object that corresponds to the specified identifier is no more available (e.g. an expired document).                                                              |
| 422  | Unprocessable Entity | Request and parameter are OK but it can't be processed due to inappropriate or corrupted data (e.g. corrupted document template, wrongly formatted document data, unknown processing command etc.). |
| 423  | Locked               | Request and parameter are OK but it can't be processed because a required object is already in processing by another task. The request can succeed if it is repeated later.                         |
| 5xx  | server error         | The service is currently in an invalid state (during startup or shutdown on in case of fatal problems with database, network or file system).                                                       |

## Headers

For some functions, the payload already contains binary data (e.g. "create document"). Accompanying information is often provided in headers, e.g. the `link` header provides the object identification. See also the `content-` headers. For example, the response with a created staged document contains the URL with the unique document identification, provided document format (MIME content type) and suggested content file name:

```
content-disposition: attachment; filename="DemoDoc10_PDFA.pdf" 
content-type: application/pdf 
link: <document/dbc82ff0-26fb-4648-8ea9-d61297370836>; rel="next"
```

## Error messages

In case of an error or even if a request is processed successfully, it can contain warnings or error messages as a part of the **response payload**. Example:

```json
{
  "hasErrors": true,
  "hasOnlyRetryableErrors": false,
  "hasWarnings": false,
  "messages": [
    {
      "messageType": "ERROR",
      "messageIdentCode": "EMPTY_MANDATORY_FIELD",
      "messageTexts": [
        {
          "languageISOCode": "en",
          "text": "'request.xmlData/jsonData' must be filled."
        }
      ],
      "indentationLevel": 0
    }
  ]
}
```

## hasErrors

Indicates that the operation couldn't be successfully performed. That could be because of:

- A non-retriable **basic issue** like syntax error (wrong URL and/or parameter), missing or invalid parameter, validation or processing errors. Such requests must be corrected before possible resubmission.
- A retriable **temporary issue** like service unavailability, timeouts, access locking or pending tasks. These requests can succeed when resubmitted later.

## hasOnlyRetryableErrors

Indicates that all errors are retriable, e.g. some data was locked in other processes or some necessary resources are currently blocked. You can **repeat** your request a bit later.

## hasWarnings

One or more warnings are returned if the operation could be performed but the result might be incomplete because of missing parameter, temporary state of the participating resources etc.