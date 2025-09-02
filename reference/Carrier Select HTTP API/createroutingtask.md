---
title: createRoutingTask
excerpt: >-
  Creates a new routing task and returns a unique task id.<br> <br> In case of
  successful creation, the response will contain the unique taskId of the
  created routing task. The respective routing task can be found by this task
  id. Proposal calculation starts in an asynchronous process. The current state
  of calculation can be request by handing over the provided task id via the
  call of getRoutingTaskResult(GetRoutingTaskResultRequestDTO).<br>
api:
  file: carrier-select-http-api-1.json
  operationId: createRoutingTask
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---