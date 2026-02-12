---
title: waitForRoutingTaskResult
excerpt: >-
  Waits for the task calculation to finish and returns a sorted list of
  proposals for the provided task id and its current calculation state.<br> <br>
  If the calculation takes longer than the set waiting time limit, the list of
  proposals will be returned in its current unfinished calculation state as soon
  as the limit is reached.<br> <br> The final list of proposals is ranked
  according to a rating profile. A rating profile uses supplements for score
  calculation and ranking.<br><br>Possible states of calculation are:<br>-
  INPROGRESS: entries (and ordering) might change in future calls. <br>- RANKED:
  ordering and entries fixed, at least one supplement missing. <br>- COMPLETE:
  ordering and entries fixed, all supplements are calculated. <br><br>A new
  routing task can be created by using
  createRoutingTask(CreateRoutingTaskRequestDTO).<br>
api:
  file: carrier-select-http-api.json
  operationId: waitForRoutingTaskResult
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---