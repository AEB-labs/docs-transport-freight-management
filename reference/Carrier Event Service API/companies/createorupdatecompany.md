---
title: /companies/{id}
excerpt: >-
  Create or update a company with the specified ID (company number). If the
  company with the given ID does not exist, a new company is created. If the
  company exist, the existing company is fully updated. Not filled fields in the
  request are treated thereby as empty data fields and lead to empty fields in
  an already existing company. It is therefore recommended to use the
  GET/companies to check whether a company with a specific ID exists or not
  BEFORE you use PUT/companies/{id}.
api:
  file: openapi_v3.json
  operationId: createOrUpdateCompany
hidden: false
---