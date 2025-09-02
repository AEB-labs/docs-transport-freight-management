---
title: getRoutingTaskResult
excerpt: >-
  Returns a sorted list of proposals for the provided task id and its current
  calculation state.<br> <br> The final list of proposals is ranked according to
  a rating profile. A rating profile uses supplements for score calculation and
  ranking.<br> <br> Possible states of calculation are:<br> - INPROGRESS:
  entries (and ordering) might change in future calls. <br> - RANKED: ordering
  and entries fixed, at least one supplement missing. <br> - COMPLETE: ordering
  and entries fixed, all supplements are calculated. <br> <br> A new routing
  task can be created by using
  createRoutingTask(CreateRoutingTaskRequestDTO).<br>
api:
  file: carrier-select-http-api-1.json
  operationId: getRoutingTaskResult
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---