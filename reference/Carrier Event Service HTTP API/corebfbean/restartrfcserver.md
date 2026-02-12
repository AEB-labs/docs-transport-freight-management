---
title: /CoreBFBean/restartRFCServer
excerpt: >-
  This method is only usefull to be called from SAP via RFC. It will restart the
  RFCServer which receives this method call. This method is useful to be called
  from SAP, if within SAP some structure definitions had changed, e.g. after
  installing a transport. The RFC name of this function is
  \"/AEB/XNSG_IF_RSTRFCSRV\".
api:
  file: carrier-event-service-http-api.json
  operationId: restartRFCServer
hidden: false
---