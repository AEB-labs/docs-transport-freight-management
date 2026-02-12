---
title: queryDocumentsById
excerpt: >-
  <h3>Query information on existing documents</h3><p>Executes a search query on
  the documents stored in the document storage. Only the documents that are
  visible to the caller (session user and session client) are returned. The
  results can be sorted by predefined criteria, the limit of the number of
  results is configurable, too.</p><h4>Date time interval range
  filter</h4><p>Use one of the given attributes to pass the filter. If more than
  one attribute is filled attributes will be used in the following order:
  relative interval, absolute interval<ul><li>Filter relative to current day,
  e.g: from 2 months ago to a week ago (relativeFrom = "-2 MONTHS", relativeTo =
  "-1 WEEKS")</li><li>Filter with absolute date-time values, see field
  examples</li></ul></p>
api:
  file: document-service-http-api.json
  operationId: queryDocumentsById
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---