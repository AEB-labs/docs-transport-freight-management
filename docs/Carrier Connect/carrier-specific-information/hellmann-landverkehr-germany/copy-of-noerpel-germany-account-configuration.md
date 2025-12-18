---
title: 'Hellmann (Germany): Account Configuration'
deprecated: false
hidden: false
metadata:
  robots: index
---
<CCOConfiguringCarriersInCarrierConnect />

To create a new Hellmann account in Carrier Connect, open Hellmann in _Master data > Carrier configurations_. In the tab _Accounts_ click on _New_.

Select account type

* (1) HELL_SAE_STD: This is the standard account type for outbound shipments.
* (2) HELLSAE_PICKUP:  **Only** use it if you will use the value-added service **Pickup Booking** (HELL_PICKUP).

<Image align="center" border={false} src="https://files.readme.io/72c81b2bdfdbd4f63aaeaeffcec9e5c52b2ad303815fb8ea6c4135e6b0578f0e-account-type.png" />

<CCOAccountTransfer />

<br />

# Hellmann (Germany) account

<Image align="center" border={false} src="https://files.readme.io/10ce444029d5512f2647e30289b5f1159fd4206d1f98fdde0f5196b0fd7ba79d-account1.png" />

<Image align="center" border={false} src="https://files.readme.io/ae2da4c9d280b821234d903a696dd5bc38bb63f1d882e2d6a2ec889b81bc7782-account2.png" />

<br />

| Number | Field                | Comment                                                                                                                                                                  |
| :----- | :------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1      | Shipper              | The address of the shipper                                                                                                                                               |
| 2      | Carrier address      | The address of the carrier (depot)                                                                                                                                       |
| 3      | Condition            | See our <Anchor label="user guide" target="_blank" href="https://docs.aeb.com/doc/cm-620065803-801708043-de-DE/t-801708043-709043211-de-DE">user guide</Anchor>          |
| 4      | Single pkg. handling | See [Single Package Handling](https://transport-freight-management.docs.developers.aeb.com/docs/copy-of-noerpel-germany-account-configuration#single-package-handling-3) |
| 5      | Customer no.         | Assigned by the carrier                                                                                                                                                  |
| 6      | GS1 base no.         | Your company's GS1 base number                                                                                                                                           |
| 7      | Package no. range    | See [Package number range](https://transport-freight-management.docs.developers.aeb.com/docs/copy-of-noerpel-germany-account-configuration#package-number-range-1)       |
| 8      | EDI transmission     | Set to _Send and log_                                                                                                                                                    |

<CCOSinglePackageHandling />

<br />

<br />

<CCOPackageNumberRange />

<br />

| Number | Field          | Comment                                                                |
| :----- | :------------- | :--------------------------------------------------------------------- |
| 1      | Abbreviation   | Choose a descriptive abbreviation. E.g. NOERPEL_PCK                    |
| 2      | Name           | Choose a descriptive name. E.g. Noerpel (Germany) package number range |
| 3      | Start value    | Assigned by the carrier                                                |
| 4      | Max. value     | Assigned by the carrier                                                |
| 5      | Auto. re-start | Activated                                                              |
| 6      | Leading zeros  | Activated                                                              |
| 7      | Char. length   | 7                                                                      |

<br />

# EDI setup

In this section the EDI upload parameters are configured.

<CCOEDINumberRange />

<br />

| Number | Field          | Comment                                                   |
| :----- | :------------- | :-------------------------------------------------------- |
| 1      | Abbreviation   | Choose a descriptive abbreviation. E.g. HELLMANN_EDI      |
| 2      | Name           | Choose a descriptive name. E.g. Hellmann EDI number range |
| 3      | Start value    | 1                                                         |
| 4      | Max. value     | 999                                                       |
| 5      | Auto. re-start | Activated                                                 |
| 6      | Leading zeros  | Activated                                                 |
| 7      | Char. length   | 3                                                         |
