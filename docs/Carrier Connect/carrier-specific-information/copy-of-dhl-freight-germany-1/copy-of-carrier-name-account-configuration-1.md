---
title: Copy of [Carrier Name] Account Configuration
deprecated: false
hidden: true
metadata:
  robots: index
---
# DSV Air Freight (Europe): Account Configuration

> For general information about how to configure a carrier in Carrier Connect, refer to our [User Guide](https://transport-freight-management.docs.developers.aeb.com/docs/carrier-connect-user-guide/) ([German version](https://transport-freight-management.docs.developers.aeb.com/docs/carrier-connect-user-guide-de/)).

## How to create the account

To create a new DSV Air Freight (Europe) account in Carrier Connect, open the carrier under **Master data > Carrier configurations**. In the tab **Accounts**, click on **New**.

## Select account type

When creating the account, select the account type as specified by DSV.

| Number | Type label                                        | Comment                                  |
| ------ | ------------------------------------------------- | ---------------------------------------- |
| 1      | DSVAIR_API2 (DSV Luftfracht API Standard-Account) | Standard account type; must be used.     |
| 2      | DSVAIR_APITRACK2 (DSV Luftfracht Account …)       | Deprecated; do not use for new accounts. |

## DSV Air Freight (Europe) account

| Number | Field                                   | Comment                                                                                                                                                          |
| ------ | --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1      | Shipper                                 | The address of the shipper.                                                                                                                                      |
| 2      | Carrier address                         | The address of the carrier (depot).                                                                                                                              |
| 3      | Condition                               | See our <Anchor label="user guide" target="_blank" href="https://docs.aeb.com/doc/cm-620065803-801708043-de-DE/t-801708043-709043211-de-DE">user guide</Anchor>. |
| 4      | Single pkg. handling                    | See [Single Package Handling](https://transport-freight-management.docs.developers.aeb.com/docs/dhlfreight-account-configuration#single-package-handling).       |
| 5      | Package no. range                       | See [Package number range](https://transport-freight-management.docs.developers.aeb.com/docs/copy-of-ups-emea-carrier-configuration#package-number-range).       |
| 6      | EDI transmission                        | Set to *Send and log*.                                                                                                                                           |
| 7      | Customer no.                            | Assigned by the carrier.                                                                                                                                         |
| 8      | GS1 base no.                            | Your company’s GS1 base number.                                                                                                                                  |
| 9      | Test user name                          | Assigned by the carrier.                                                                                                                                         |
| 10     | Test password                           | Assigned by the carrier.                                                                                                                                         |
| 11     | Test subscription key                   | Assigned by the carrier.                                                                                                                                         |
| 12     | Test subscription key (Document upload) | Assigned by the carrier.                                                                                                                                         |
| 13     | Test auth sub. key                      | Assigned by the carrier.                                                                                                                                         |

## Package number range

<CCOPackageNumberRange />
