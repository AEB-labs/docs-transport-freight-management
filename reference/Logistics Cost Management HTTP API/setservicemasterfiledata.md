---
title: setServiceMasterFileData
excerpt: >-
  Create or update multiple Services in the Billing engine.<br> Create or update
  multiple services in the master file data of the engine. Because of
  performance and transactional issues it is recommended to transfer about 100
  services within one synchronous call. All transfered services will be either
  created or updated. The identCode and scenarioIdentCode (these are key values)
  of the service will be checked before processing. In case of any unfilled key
  value, nothing will be done. In case of other problems for a single service
  e.g locking or invalid identCode values the processing is usually continued
  with the next service, skipping, the problematic service. This means the
  record will be skipped completely and processing will continue with the next
  service. Anyway such errors will set the hasErrors or hasWarnings to true. To
  analyse situations check the response for details. Possible messageIdentCodes
  are documented in AbstractResponseDTO, BSetServiceMasterFileDataResponseDTO,
  BServiceMFResultDTO, AbstractResponseItemDTO and BServiceMFResultDTO
api:
  file: logistics-cost-management-http-api.json
  operationId: setServiceMasterFileData
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---