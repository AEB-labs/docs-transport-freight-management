---
title: Printing
excerpt: Requirements of the printing API and how to use it.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Created documents can be passed directly to your printers. In order to automate printing as much as possible, i.e. to print  in the background without user interaction, some prerequisites need to be met. 

# Prerequisites

1. In order to print documents in the background the *AEB Cloud Printing Service* needs to be installed and configured in your location so the *Document Service* can directly reach your printers.\
   :information_source: For installation and more detail contact *AEB Technical Services* .
2. Currently, printing is only supported for the [staged document instances](doc:staged-document-instances). The reason is that certain *output settings* need to be completed manually in the context of the associated <Glossary>Document type</Glossary>s.\
   :information_source: See chapter [Output Settings](doc:output-settings) for more details.

> 📘 Note that the printing cannot be fully tested with our demo system because there are no printers configured. Email notifications are restricted, as well.

# Create a Print Request

To print a document, you need its `documentId`. Printing is only supported for staged document instances with a valid <Glossary>Document type</Glossary> reference.

The individual print requests are collected into sequential queues (per user or — if configured — per workstation). Successfully finished requests are cleaned up on a daily basis, i.e. successfully executed print requests are not stored but deleted daily.

## Try it out

Use this [print request](/reference/printdocumentinstance) or [Swagger UI](https://rz3.aeb.de/demo1docs/swagger/#/DocumentService/printDocumentInstance). Fill in the `documentId` and issue the request.

By default, the queue and *output settings* of the requesting user/client are used. When `workstationId` is specified, the *output settings* associated with the  corresponding configured workstation are applied and the request is added to the workstation queue.

Some of the configured *output settings (for print)* can be overwritten in the individual requests:

* If `stopOnError` is enabled, further print requests in the queue are blocked from being processed in case of a printing error of the issued request. If it is disabled, a printing error does not prevent other print requests from processing. This option can be used to control the proper sort order of print requests and pause the whole queue until the printing error is solved.
* If `monitorPrintJob`  is enabled, the actual printing process is monitored after the rendered print job has been accepted by the printer spooler. The print request is considered successful only when the printer driver has confirmed the entire print operation. If it is disabled, the request is considered successful when the print job has been accepted by the printer spooler. This option can be used to ensure that the data has been physically accepted by the printer.
* If `notificationEmail` is filled, an email is generated for the recipient in case of printing errors.
* If `notificationDisabled` is activated, no email notifications are generated even if there is a notification email configured in the *output settings*.

You get a response like this:

```json
{
  "hasErrors": false,
  "hasOnlyRetryableErrors": false,
  "hasWarnings": false,
  "messages": [],
  "state": "SUCCESS",
  "printRequestId": "49CC4DAF86FF4F0385679DEFCE254C14"
}
```

The requests is now in the queue and its processing is triggered in the background.

# Monitor Print Requests

You should always use the `printRequestId` returned from an issued print request to follow up the state of the print request or configure the notification email to get informed in case of problems. Even if the request is successfully accepted, it can fail for several reasons when it comes to the actual execution, e.g.:

* the document has expired or its printable content is missing
* the output settings are incomplete or invalid
* there are no printers available (the cloud printing service is not connected)
* the document content has been generated for a different printer type (applies to labels)
* the specified printer is not available or offline at the moment of printing

Such situations usually require manual correction. The queued request can be then either **reset** (i.e. retry the printing again) or marked as **ignored** (i.e. skip and forget the error). For currently running print jobs with active `monitorPrintJob`, the **cancellation** can be requested (note that the cancel request is forwarded to the printer driver, so there is no guarantee that it really succeeds).

Besides using the API, the error situations can be manually corrected via the [Print Queue Application](https://API_TEST%40APITEST:API_TEST2021@rz3.aeb.de/demo1docs/rest/DocumentService/ui/printQueue?user=API_TEST\&language=en\&redirect=true) (see also chapter [User Interface](doc:user-interface#print-request-overview)):

![](https://files.readme.io/ec9a32c-image.png)

## Try it out

### Single print request state

Use the returned `printRequestId` to follow up the state of the issued print request by calling [print request query](/reference/getprintrequest) or [Swagger UI](https://rz3.aeb.de/demo1docs/swagger/#/DocumentService/getPrintRequest).

By default, requests belonging to the queue of the requesting user/client is returned. When `workstationId` is specified, requests of the queue of the corresponding configured workstation are returned.

You get a response like this:

```json
{
  "hasErrors": false,
  "hasOnlyRetryableErrors": false,
  "hasWarnings": false,
  "messages": [],
  "printRequestId": "49CC4DAF86FF4F0385679DEFCE254C14",
  "documentId": "ceac6b34-f66b-45d3-81d0-c3185bc5efc8",
  "stopOnError": false,
  "isIgnored": false,
  "state": "ERROR",
  "stateMessage": "There is currently no active Service Agent available. Documents cannot be printed.",
  "requestedAt": "2023-11-21T13:20:21",
  "lastAccessedAt": "2023-11-21T13:20:21"
}
```

This error message signals that the request has failed because there are no printers available (cloud printing service is not connected).

### All print requests overview

To get an overview of all your print requests, call the [print requests](/reference/getprintrequests) or use [Swagger UI](https://rz3.aeb.de/demo1docs/swagger/#/DocumentService/getPrintRequests). You can apply a filter for requests that are already finished (`onlyActive` = true/false) and/or restrict the result only to recent requests by setting the issue time limit (`requestedAtAfter`).

### Modify print request state

Use the returned `printRequestId` (and `workstationId` if applicable) to modify the state of the issued print request by calling [update request](/reference/updateprintrequest) or [Swagger UI](https://rz3.aeb.de/demo1docs/swagger/#/DocumentService/updatePrintRequest).

The `action` parameter allows one of the following values:

* `CANCEL` - issue a cancel request. Applicable only when the print request is currently in processing. When the cancellation is processed successfully, the print request state eventually changes to **ERROR**. Optionally, the `timeout` parameter can be specified to limit the time to wait for the response.
* `IGNORE` - set a previously failed request to the "ignored" state (i.e. not blocking your print queue).
* `RESET` - reset  a previously failed request. The requests will become ready to be processed again.

### Delete print request

Use the returned `printRequestId` (and `workstationId` if applicable) to delete an obsolete print request by calling [delete request](/reference/deleteprintrequest) or [Swagger UI](https://rz3.aeb.de/demo1docs/swagger/#/DocumentService/deletePrintRequest).
