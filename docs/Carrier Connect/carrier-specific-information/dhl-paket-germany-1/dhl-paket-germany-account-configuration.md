---
title: 'DHL Paket (Germany): Account Configuration'
deprecated: false
hidden: false
metadata:
  robots: index
---
<CCOConfiguringCarriersInCarrierConnect />

To create a new DHL Paket Deutschland account in Carrier Connect, open DHL Paket Deutschland in _Master data > Carrier configurations_. In the tab _Accounts_ click on _New_.

Select account type

* (1) DHLEXPINT_MYDHLAPIV2 **only** if you will use the value-added service **Pickup Booking** (DHLEXPINTPICKUP).
* (2) DHLEXPINT_STD_IFTMIN in all other cases. It's the standard account type for outbound shipments.

# DHL Freight account

<Image align="center" src="https://files.readme.io/192820f3023744b86bd1007e1acb84582472307308b1b522e4f9a6e52ce1c249-dhlfreight_account1.png" />

<Image align="center" src="https://files.readme.io/6aaf090c3171d81ef4947d6421c2b9b1fb2c61f15bd9c8c7fb9c643394ea9c63-dhlfreight_account2.png" />

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Number
      </th>

      <th>
        Field
      </th>

      <th>
        Comment
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        1
      </td>

      <td>
        Shipper
      </td>

      <td>
        The address of the shipper
      </td>
    </tr>

    <tr>
      <td>
        2
      </td>

      <td>
        Carrier address
      </td>

      <td>
        The address of the carrier (depot)
      </td>
    </tr>

    <tr>
      <td>
        3
      </td>

      <td>
        Condition
      </td>

      <td>
        See our <Anchor label="user guide" target="_blank" href="https://docs.aeb.com/doc/cm-620065803-801708043-de-DE/t-801708043-709043211-de-DE">user guide</Anchor>
      </td>
    </tr>

    <tr>
      <td>
        4
      </td>

      <td>
        Single pkg. handling
      </td>

      <td>
        See [Single Package Handling](https://transport-freight-management.docs.developers.aeb.com/docs/dhlfreight-account-configuration#single-package-handling)
      </td>
    </tr>

    <tr>
      <td>
        5
      </td>

      <td>
        Customer number
      </td>

      <td>
        Assigned by the carrier
      </td>
    </tr>

    <tr>
      <td>
        6
      </td>

      <td>
        Depot number
      </td>

      <td>
        Assigned by the carrier
      </td>
    </tr>

    <tr>
      <td>
        7
      </td>

      <td>
        Package no. range
      </td>

      <td>
        See [Package number range](https://transport-freight-management.docs.developers.aeb.com/docs/copy-of-ups-emea-carrier-configuration#package-number-range)
      </td>
    </tr>

    <tr>
      <td>
        8
      </td>

      <td>
        EDI transmission
      </td>

      <td>
        Set to _Send and log_
      </td>
    </tr>

    <tr>
      <td>
        9
      </td>

      <td>
        Tracking no. type
      </td>

      <td>
        Assigned by the carrier. There are two options:

        * ANSIFact ASC MH 10
        * GS1 EAN 128 Licenseplate

        See [Tracking no. type](https://transport-freight-management.docs.developers.aeb.com/docs/copy-of-ups-emea-carrier-configuration#tracking-no-type)
      </td>
    </tr>
  </tbody>
</Table>

<CCOSinglePackageHandling />

<br />

<CCOPackageNumberRange />

<br />

| Number | Field          | Comment                                                          |
| :----- | :------------- | :--------------------------------------------------------------- |
| 1      | Abbreviation   | Choose a descriptive abbreviation. E.g. DHLFREIGHT_PCK           |
| 2      | Name           | Choose a descriptive name. E.g. DHL Freight package number range |
| 3      | Start value    | 1                                                                |
| 4      | Max. value     | 999999999                                                        |
| 5      | Auto. re-start | Activated                                                        |
| 6      | Leading zeros  | Activated                                                        |
| 7      | Char. length   | 9                                                                |

## Tracking no. type

### ANSIFact ASC MH 10

![](https://files.readme.io/16cbe88a7f6174ba37b1b0eee61030233af0cdd094517732b35ca91d7b2906d7-image.png)

| Number | Field        | Comment                 |
| :----- | :----------- | :---------------------- |
| 1      | Dispose area | Assigned by the carrier |

### GS1 EAN 128 Licenseplate

![](https://files.readme.io/dcf87f87eac2a3cacdd22cc337059d6c133c523d32fe6babdeb1977cb9036ce1-image.png)

| Number | Field | Comment                                          |
| :----- | :---- | :----------------------------------------------- |
| 1      | GLN   | The GS1 base number of your company (7-9 digits) |

<br />

# EDI setups

In this section the EDI upload parameters are configured.

![](https://files.readme.io/6614a386d5cd2caeb0efbf299999ed3f26ffb6e9e724de9b678adb30948265e1-image.png)

<br />

| Number | ID       | Comment                                                                                |
| :----- | :------- | :------------------------------------------------------------------------------------- |
| 1      | PICKUP   | Only needed if you use the value added service **Pickup booking (DHLFREIGHTPICKBOOK)** |
| 2      | STANDARD | This will send the standard EDI (when closing the pickup)                              |
| 3      | RETURN   | Only needed if you use the value added service **Return booking (DHLFREIGHTRETBOOK)**  |

Select the EDI ID you want to configure and click on _Open_.

![](https://files.readme.io/a4c145eec2a59f415d2db6a0c15752fa9136d5198eb9b9f158b1cf0d3f0eb1ef-image.png)

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
