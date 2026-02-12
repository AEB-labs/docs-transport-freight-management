---
title: /SyncBFBean/synchronizeEvents
excerpt: >-
  Poll the next events for the client system.<br> This method requires the
  client system to persist the synchronisation state itself and passing a proper
  value for {@link SyncEventsRequestDTO#syncId}<br> See {@link
  #getNotAcknowledgedEvents(SyncEventsRequestDTO)} for a version of the method,
  were the syncronisation state is kept within the Engine.
api:
  file: openapi_v3.json
  operationId: synchronizeEvents
hidden: false
---