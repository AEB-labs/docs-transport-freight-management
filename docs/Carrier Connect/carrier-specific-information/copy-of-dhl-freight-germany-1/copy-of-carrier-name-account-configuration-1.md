---
title: 'DSV Air Freight (Europe): Account Configuration'
deprecated: false
hidden: false
metadata:
  robots: index
---
<CCOConfiguringCarriersInCarrierConnect />

To create a new DSV Air Freight (Europe) account in Carrier Connect, open DSV Air Freight (Europe) in _Master data > Carrier configurations_. In the tab _Accounts_ click on _New_.

Select account type DSVAIR_API2.

<Image align="center" border={false} src="https://files.readme.io/0b2dd5954313fb70b6b5534ba6c0a4141f2b27a9812b89ad95aca70e03959b87-AccountType.png" />

<CCOAccountTransfer />

<br />

# DSV Air Freight (Europe) account

<Image align="center" border={false} src="https://files.readme.io/f6c9457d987bc6e839a527689a9b625b9e3d5aac74d1f9ecd3e4046bf09f0b53-DSV_AIR1.png" />

<Image align="center" border={false} src="https://files.readme.io/03332821970dfa7ed0732881224aeb457c9a64c56152bfaa7ecbc28beaf21c12-DSV_AIR2.png" />

<Image align="center" border={false} src="https://files.readme.io/e3041664162029e43e5f090b6828ed9caeb68a03f4ba8fed031b40a5c7940e33-DSV_AIR3.png" />

<Image align="center" border={false} src="https://files.readme.io/1a861bfa23863c2ac676be47d0803791d6d204394fd6852db44501e193b2cf09-DSV_AIR4.png" />

| Number | Field                                    | Comment                                                                                                                                                              |
| :----- | :--------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1      | Shipper                                  | The address of the shipper                                                                                                                                           |
| 2      | Carrier address                          | The address of the carrier (depot)                                                                                                                                   |
| 3      | Condition                                | See our <Anchor label="user guide" target="_blank" href="https://docs.aeb.com/doc/cm-620065803-801708043-de-DE/t-801708043-709043211-de-DE">user guide</Anchor>      |
| 4      | Customer no.                             | Assigned by the carrier                                                                                                                                              |
| 5      | GS1 base no.                             | Your company's GS1 base number                                                                                                                                       |
| 6      | Package no. range                        | See <a href="https://transport-freight-management.docs.developers.aeb.com/docs/copy-of-ups-emea-carrier-configuration#package-number-range">Package number range</a> |
| 7      | Test user name (Web service data)        | Assigned by the carrier                                                                                                                                              |
| 8      | Test password (Web service data)         | Assigned by the carrier                                                                                                                                              |
| 9      | Test subscription key (Web service data) | Assigned by the carrier                                                                                                                                              |
| 10     | Test subscription key (Document upload)  | Assigned by the carrier                                                                                                                                              |
| 11     | Test auth sub. key (Authentication)      | Assigned by the carrier                                                                                                                                              |

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