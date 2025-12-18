---
title: 'Rhenus Freight (Germany): Account Configuration'
deprecated: false
hidden: false
metadata:
  robots: index
---
<CCOConfiguringCarriersInCarrierConnect />

To create a new Rhenus Freight account in Carrier Connect, open Rhenus Freight in _Master data > Carrier configurations_. In the tab _Accounts_ click on _New_.

# Rhenus Freight (Germany) account

<Image align="center" border={false} src="https://files.readme.io/8a861f86b7dbcd7a77224c08e30b0c2d7a577ff60664ece79dbd518ccb790f68-account1.png" />

<Image align="center" border={false} src="https://files.readme.io/ae2da4c9d280b821234d903a696dd5bc38bb63f1d882e2d6a2ec889b81bc7782-account2.png" />

<br />

| Number | Field                | Comment                                                                                                                                                                 |
| :----- | :------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1      | Shipper              | The address of the shipper                                                                                                                                              |
| 2      | Carrier address      | The address of the carrier (depot)                                                                                                                                      |
| 3      | Condition            | See our <Anchor label="user guide" target="_blank" href="https://docs.aeb.com/doc/cm-620065803-801708043-de-DE/t-801708043-709043211-de-DE">user guide</Anchor>         |
| 4      | Single pkg. handling | See [Single Package Handling](https://transport-freight-management.docs.developers.aeb.com/docs/rhenus-freight-germany-account-configuration#single-package-handling-4) |
| 5      | Customer no.         | Assigned by the carrier                                                                                                                                                 |
| 6      | GS1 base no.         | Your company's GS1 base number                                                                                                                                          |
| 7      | Package no. range    | See [Package number range](https://transport-freight-management.docs.developers.aeb.com/docs/rhenus-freight-germany-account-configuration#package-number-range-2)       |
| 8      | EDI transmission     | Set to _Send and log_                                                                                                                                                   |

<CCOSinglePackageHandling />

<br />

<br />

<CCOPackageNumberRange />

<br />

| Number | Field          | Comment                                                               |
| :----- | :------------- | :-------------------------------------------------------------------- |
| 1      | Abbreviation   | Choose a descriptive abbreviation. E.g. RHENUS_PCK                    |
| 2      | Name           | Choose a descriptive name. E.g. Rhenus (Germany) package number range |
| 3      | Start value    | Assigned by the carrier                                               |
| 4      | Max. value     | Assigned by the carrier                                               |
| 5      | Auto. re-start | Activated                                                             |
| 6      | Leading zeros  | Activated                                                             |
| 7      | Char. length   | 7                                                                     |

<br />

# EDI setup

In this section the EDI upload parameters are configured.

<CCOEDINumberRange />

<br />

| Number | Field          | Comment                                                 |
| :----- | :------------- | :------------------------------------------------------ |
| 1      | Abbreviation   | Choose a descriptive abbreviation. E.g. RHENUS_EDI      |
| 2      | Name           | Choose a descriptive name. E.g. Rhenus EDI number range |
| 3      | Start value    | 1                                                       |
| 4      | Max. value     | 999                                                     |
| 5      | Auto. re-start | Activated                                               |
| 6      | Leading zeros  | Activated                                               |
| 7      | Char. length   | 3                                                       |
