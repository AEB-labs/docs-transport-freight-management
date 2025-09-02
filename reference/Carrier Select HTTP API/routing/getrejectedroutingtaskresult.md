---
title: getRejectedRoutingTaskResult
excerpt: >-
  Returns a sorted list of the rejected proposals for the provided task id and
  its current calculation state.<br> The rejected proposals are those proposals
  which were filtered out according to the settings in the rating profile.<br>
  <br> Possible states of calculation are:<br> - INPROGRESS: entries (and
  ordering) might change in future calls. <br> - RANKED: ordering and entries
  fixed, at least one supplement missing. <br> - COMPLETE: ordering and entries
  fixed, all supplements are calculated. <br> <br> A new routing task can be
  created by using createRoutingTask(CreateRoutingTaskRequestDTO).<br>
api:
  file: carrier-select-http-api.json
  operationId: getRejectedRoutingTaskResult
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---