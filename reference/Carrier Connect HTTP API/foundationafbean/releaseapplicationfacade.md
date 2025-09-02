---
title: /FoundationAFBean/releaseApplicationFacade
excerpt: >-
  Release a application facade which is no longer needed.<br> This call will
  save resources in the server, because the server must not wait for the timeout
  of the application facades session but can release it earlier.<br> The method
  should only be called if it is definitively known, that no access to the
  application facade by the user is possible any more, e.g. because the
  surrounding client GUI window was closed.<br> The RFC name of this function is
  \"/AEB/XNSG_IF_RELAF\".
api:
  file: carrier-connect-http-api.json
  operationId: releaseApplicationFacade
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---