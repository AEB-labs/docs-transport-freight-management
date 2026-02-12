---
title: /SyncBFBean/getNotAcknowledgedEvents
excerpt: >-
  Poll any not acknowledged events for the client system.<br> This method does
  not require, that the client system fills {@link
  SyncEventsRequestDTO#syncId}.<br> However, it requires, that a call to {@link
  #acknowledgeEvents(AcknowledgeEventsRequestDTO)} is done for acknowledge of
  the events.<br> Since XNSG 4.0, Nov. FP, 2017<br>.
api:
  file: openapi_v3.json
  operationId: getNotAcknowledgedEvents
hidden: false
---