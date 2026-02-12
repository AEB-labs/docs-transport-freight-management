---
title: /FoundationAFBean/releaseApplicationFacade
excerpt: >-
  Release a UI API which is no longer needed.<br> This call will save resources
  in the server, because the server must not wait for the timeout of the UI API
  session but can release it earlier.<br> The method should only be called if it
  is definitively known, that no access to the UI API by the user is possible
  any more, e.g. because the surrounding client GUI window was closed.<br> The
  RFC name of this function is \"/AEB/XNSG_IF_RELAF\".
api:
  file: openapi_v3.json
  operationId: releaseApplicationFacade
hidden: false
---