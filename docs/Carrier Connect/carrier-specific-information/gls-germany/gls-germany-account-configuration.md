---
title: 'GLS (Germany): Account Configuration'
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
<br />

<CCOConfiguringCarriersInCarrierConnect />

To create a new GLS account in Carrier Connect, open GLS in _Master data > Carrier configurations_. In the tab _Accounts_ click on _New_.

# GLS account

<Image align="center" border={false} src="https://files.readme.io/e7e438e8dd40e2635f5fd7f1e9631c5029ead6ca876beb1ad51c9c26cbbaa211-account1.png" />

<Image align="center" border={false} src="https://files.readme.io/71293ffb8b7bea77c7e6a3aafd273e69d4c3934fe1a7808d26d945eb700948dd-account2.png" />

<br />

| Number | Field                | Comment                                                                                                                                                                                  |
| :----- | :------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1      | Shipper              | The address of the shipper                                                                                                                                                               |
| 2      | Carrier address      | The address of the carrier (depot)                                                                                                                                                       |
| 3      | Condition            | See our <Anchor label="user guide" target="_blank" href="https://docs.aeb.com/doc/cm-620065803-801708043-de-DE/t-801708043-709043211-de-DE">user guide</Anchor>                          |
| 4      | Single pkg. handling | See [Single Package Handling](https://transport-freight-management.docs.developers.aeb.com/docs/dhlfreight-account-configuration#single-package-handling)                                |
| 5      | Customer no.         | Assigned by the carrier                                                                                                                                                                  |
| 6      | EDI transmission     | Set to _Send and log_                                                                                                                                                                    |
| 7      | Contact ID           | Assigned by the carrier                                                                                                                                                                  |
| 8      | Alt. server URL      | Assigned by the carrier. The URL used for the GLS webservice. It looks like this: https://shipit-wbm-de01.gls-group.eu:8443/backend/ShipmentProcessingService/ShipmentProcessingPortType |
| 9      | Operating mode       | Choose _Test_, if you are in the test environment. Choose _Productive_, if you are in the productive environment.                                                                        |
| 10     | User                 | Assigned by the carrier                                                                                                                                                                  |
| 11     | Password             | Assigned by the carrier                                                                                                                                                                  |