---
title: 'Noerpel (Germany): Account Configuration'
deprecated: false
hidden: false
metadata:
  robots: index
---
<CCOConfiguringCarriersInCarrierConnect />

To create a new Noerpel account in Carrier Connect, open Noerpel in _Master data > Carrier configurations_. In the tab _Accounts_ click on _New_.

Select account type

* (1) NOERPEL_ABHBORD **only** if you will use the value-added service **Pickup Booking** (PICKUP_BOOKING).
* (2) NOERPEL_STDBORD in all other cases. It's the standard account type for outbound shipments.

<Image align="center" border={false} src="https://files.readme.io/63058aa7976e714baeab2afe7821493afb87e2e2c500abd63ba1977c2d955b2a-account-type.png" />

<CCOAccountTransfer />

<br />

# Noerpel (Germany) account

<Image align="center" border={false} src="https://files.readme.io/0b97c062b1f5dd189306e37dad5f31bcb7254d47d368a5073bf3772fdf4b8f31-account1.png" />

<Image align="center" border={false} src="https://files.readme.io/39c14ff843098ffff0db396b8c8c7d3dde22b5f391583e1727a845b090696342-account2.png" />

<br />

| Number | Field                | Comment                                                                                                                                                              |
| :----- | :------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1      | Shipper              | The address of the shipper                                                                                                                                           |
| 2      | Carrier address      | The address of the carrier (depot)                                                                                                                                   |
| 3      | Condition            | See our <Anchor label="user guide" target="_blank" href="https://docs.aeb.com/doc/cm-620065803-801708043-de-DE/t-801708043-709043211-de-DE">user guide</Anchor>      |
| 4      | Single pkg. handling | See [Single Package Handling](https://transport-freight-management.docs.developers.aeb.com/docs/noerpel-germany-account-configuration#single-package-handling-1)     |
| 5      | Customer no.         | Assigned by the carrier                                                                                                                                              |
| 6      | Depot no.            | Assigned by the carrier                                                                                                                                              |
| 6      | Package no. range    | See <a href="https://transport-freight-management.docs.developers.aeb.com/docs/copy-of-ups-emea-carrier-configuration#package-number-range">Package number range</a> |
| 7      | Ship. no. range      | Assigned by the carrier. Usually 6 digits. This is used as the fixed part of the tracking number.                                                                    |
| 8      |                      |                                                                                                                                                                      |
| 9      |                      |                                                                                                                                                                      |

<CCOSinglePackageHandling />

<br />

<br />

<CCOPackageNumberRange />

<br />

| Number | Field          | Comment                                                                       |
| :----- | :------------- | :---------------------------------------------------------------------------- |
| 1      | Abbreviation   | Choose a descriptive abbreviation. E.g. DSVAIR_PCK                            |
| 2      | Name           | Choose a descriptive name. E.g. DSV Air Freight (Europe) package number range |
| 3      | Start value    | 1                                                                             |
| 4      | Max. value     | 999.999.999                                                                   |
| 5      | Auto. re-start | Activated                                                                     |
| 6      | Leading zeros  | Activated                                                                     |
| 7      | Char. length   | 9                                                                             |
