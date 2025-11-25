---
title: 'Dachser Road Freight (Europe): Account Configuration'
deprecated: false
hidden: true
metadata:
  robots: index
---
<CCOConfiguringCarriersInCarrierConnect />

To create a new Dachser Road Freight account in Carrier Connect, open Dachser Road Freight (Dachser Landverkehr Europa) in _Master data > Carrier configurations_. In the tab _Accounts_ click on _New_.

# Dachser account

When creating a new Dachser account, you can choose between two account types:

<Image border={false} src="https://files.readme.io/911a9dac0c2326d7168ecf08b068b1c15eb4e24361d720a63f62ec6276312090-image.png" />

| Account Type          | Description                                                                                                                 |
| :-------------------- | :-------------------------------------------------------------------------------------------------------------------------- |
| DACHSER_STD           | The standard account type for outbound shipments                                                                            |
| DACHSER_PICKUPBOOKING | When using the value-added service **Collection booking (PICKUPBOOKING)** you have to create this account type additionally |

<CCOAccountTransfer />

<Image align="center" border={false} src="https://files.readme.io/85fa1b3f45eb08f572b9dcb8d61c8c761a1c3585dc0c475680df7616cb484f18-DACHSER1.png" />

<Image align="center" border={false} src="https://files.readme.io/1b506e0a81318ec948fa1778146897f813799b8f4b8225db82e441b69b2137ec-DACHSER2.png" />

<br />

| Number | Field                | Comment                                                                                                                                                         |
| :----- | :------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1      | Shipper              | The address of the shipper                                                                                                                                      |
| 2      | Carrier address      | The address of the carrier (depot)                                                                                                                              |
| 3      | Condition            | See our <Anchor label="user guide" target="_blank" href="https://docs.aeb.com/doc/cm-620065803-801708043-de-DE/t-801708043-709043211-de-DE">user guide</Anchor> |
| 4      | Single pkg. handling | See [Single Package Handling](https://transport-freight-management.docs.developers.aeb.com/docs/dhlfreight-account-configuration#single-package-handling)       |
| 5      | Customer number      | Assigned by the carrier                                                                                                                                         |
| 6      | Depot number         | Assigned by the carrier                                                                                                                                         |
| 7      | GS1 base no.         | Your company's GS1 base number                                                                                                                                  |
| 8      | Package no. range    | See [Package number range](https://transport-freight-management.docs.developers.aeb.com/docs/copy-of-ups-emea-carrier-configuration#package-number-range)       |
| 9      | EDI transmission     | Set to _Send and log_                                                                                                                                           |
| 10     | Document upload      | If you want to transmit documents to Dachser electronically, set to _Send and log_                                                                              |
| 11     | Doc. upl. connection | From the dropdown choose _DOCUPLOAD_                                                                                                                            |
| 12     | API key              | Assigned by the carrier                                                                                                                                         |

<CCOSinglePackageHandling />

<br />

<CCOPackageNumberRange />

<br />

| Number | Field          | Comment                                                                                                |
| :----- | :------------- | :----------------------------------------------------------------------------------------------------- |
| 1      | Abbreviation   | Choose a descriptive abbreviation. E.g. DACHSER_PCK                                                    |
| 2      | Name           | Choose a descriptive name. E.g. DACHSER package number range                                           |
| 3      | Start value    | Assigned by the carrier                                                                                |
| 4      | Max. value     | Assigned by the carrier                                                                                |
| 5      | Auto. re-start | Activated                                                                                              |
| 6      | Leading zeros  | Activated                                                                                              |
| 7      | Char. length   | Between 7 and 9, depending on the length of your GS1 base number (in total both numbers must equal 16) |

<br />

# EDI setups

In this section the EDI upload parameters are configured.

<Image border={false} src="https://files.readme.io/6614a386d5cd2caeb0efbf299999ed3f26ffb6e9e724de9b678adb30948265e1-image.png" />

<br />

| Number | ID       | Comment                                                                                |
| :----- | :------- | :------------------------------------------------------------------------------------- |
| 1      | PICKUP   | Only needed if you use the value added service **Pickup booking (DHLFREIGHTPICKBOOK)** |
| 2      | STANDARD | This will send the standard EDI (when closing the pickup)                              |
| 3      | RETURN   | Only needed if you use the value added service **Return booking (DHLFREIGHTRETBOOK)**  |

Select the EDI ID you want to configure and click on _Open_.

<Image border={false} src="https://files.readme.io/a4c145eec2a59f415d2db6a0c15752fa9136d5198eb9b9f158b1cf0d3f0eb1ef-image.png" />

| Number | Field          | Comment                                                                                                                                                                 |
| :----- | :------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1      | EDI no. range  | The EDI number range. See [EDI number range](https://transport-freight-management.docs.developers.aeb.com/docs/copy-of-ups-emea-carrier-configuration#edi-number-range) |
| 2      | EDI connection | The SFTP-Parameters used for the EDI upload. See                                                                                                                        |

<br />

<CCOEDINumberRange />

<br />

| Number | Field          | Comment                                                      |
| :----- | :------------- | :----------------------------------------------------------- |
| 1      | Abbreviation   | Choose a descriptive abbreviation. E.g. DHLFREIGHT_EDI       |
| 2      | Name           | Choose a descriptive name. E.g. DHL Freight EDI number range |
| 3      | Start value    | 1                                                            |
| 4      | Max. value     | 999                                                          |
| 5      | Auto. re-start | Activated                                                    |
| 6      | Leading zeros  | Activated                                                    |
| 7      | Char. length   | 3                                                            |

<br />
