---
title: 'DHL Freight (Germany): Account Configuration'
deprecated: false
hidden: false
metadata:
  robots: index
---
<CCOConfiguringCarriersInCarrierConnect />

To create a new DHL Freight account in Carrier Connect, open DHL Freight in _Master data > Carrier configurations_. In the tab _Accounts_ click on _New_.

# DHL Freight account

<Image border={false} src="https://files.readme.io/a73f400873e88050390ab874a243744feb53246f5cf9d3fcd086c99f65b10f32-image.png" />

<Image border={false} src="https://files.readme.io/901975d59003b80e956aaa21237004bf160eb59f7607201b5d23a24e43423632-image.png" />

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

      </td>
    </tr>

    <tr>
      <td>
        3
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
        4
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
        5
      </td>

      <td>
        Package no. range
      </td>

      <td>
        see [Package number range](https://transport-freight-management.docs.developers.aeb.com/docs/copy-of-ups-emea-carrier-configuration#package-number-range)
      </td>
    </tr>

    <tr>
      <td>
        6
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
        7
      </td>

      <td>
        Tracking no. type
      </td>

      <td>
        Assigned by the carrier. There are two options:

        * ANSIFact ASC MH 10
        * GS1 EAN 128 Licenseplate
      </td>
    </tr>
  </tbody>
</Table>

## Number ranges

<CCONumberRanges />

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

<Image border={false} src="https://files.readme.io/16cbe88a7f6174ba37b1b0eee61030233af0cdd094517732b35ca91d7b2906d7-image.png" />

| Number | Field        | Comment                 |
| :----- | :----------- | :---------------------- |
| 1      | Dispose area | Assigned by the carrier |

### GS1 EAN 128 Licenseplate

<Image border={false} src="https://files.readme.io/dcf87f87eac2a3cacdd22cc337059d6c133c523d32fe6babdeb1977cb9036ce1-image.png" />

| Number | Field | Comment                                          |
| :----- | :---- | :----------------------------------------------- |
| 1      | GLN   | The GS1 base number of your company (7-9 digits) |

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

## EDI number range

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

## EDI connection

<br />

<br />

<br />

## Mapping: Terms of Delivery & Packages

* [Converting terms of delivery](https://rz3.aeb.de/docudata/OnlineHelp/cai/en-US/index.html#338067211620280459)
* [Converting package types](https://rz3.aeb.de/docudata/OnlineHelp/cai/en-US/index.html#338084491620282891)
