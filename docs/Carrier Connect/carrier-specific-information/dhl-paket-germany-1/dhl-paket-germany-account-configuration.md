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

* (1) DHLPAKETSTD (DHL Paket) in all other cases. It's the standard account type for outbound shipments.
* (2) DHLPAKETWARENPOST (DHL Paket Warenpost) **only** if you will use the value-added service **DHL small parcel** (DHL_STD_WPNATIONAL).

![](https://files.readme.io/683164ca24ac4f0a3f0ac90334fe702fcfd18bbfd583228f02c78aaee6dd4cda-image.png)

<br />

# DHL Paket account

<Image align="center" src="https://files.readme.io/0c1f050fd62c09dc57bb2896e0654039dbfbc478b488cc9ecf85e944645a8bc4-acc1.png" />

<Image align="center" src="https://files.readme.io/fc755562ed32b03083c16c5e4e5e2ebdfb94aa7ed0204d44630610e6fc0035da-acc2.png" />

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
        Package center
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
        EKP number
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
        Participation
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
        See [Package number range](https://transport-freight-management.docs.developers.aeb.com/docs/dhl-paket-germany-account-configuration#package-number-range)
      </td>
    </tr>

    <tr>
      <td>
        8
      </td>

      <td>
        Sheet no. range
      </td>

      <td>
        See [Package number range](https://transport-freight-management.docs.developers.aeb.com/docs/dhl-paket-germany-account-configuration#package-number-range)
      </td>
    </tr>

    <tr>
      <td>
        9
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
        10
      </td>

      <td>
        Tracking no. type
      </td>

      <td>
        Assigned by the carrier. There are two options:

        * GS1 EAN 128 Licenseplate
        * Identcode

        See [Tracking no. type](https://transport-freight-management.docs.developers.aeb.com/docs/dhl-paket-germany-account-configuration#tracking-no-type)
      </td>
    </tr>
  </tbody>
</Table>

<br />

<CCOPackageNumberRange />

### Package number range

| Number | Field          | Comment                                                        |
| :----- | :------------- | :------------------------------------------------------------- |
| 1      | Abbreviation   | Choose a descriptive abbreviation. E.g. DHLPAKET_PCK           |
| 2      | Name           | Choose a descriptive name. E.g. DHL Paket package number range |
| 3      | Start value    | Assigned by the carrier                                        |
| 4      | Max. value     | Assigned by the carrier                                        |
| 5      | Auto. re-start | Activated                                                      |
| 6      | Leading zeros  | Activated                                                      |
| 7      | Char. length   | 3-8                                                            |

### Sheet number range

| Number | Field          | Comment                                                      |
| :----- | :------------- | :----------------------------------------------------------- |
| 1      | Abbreviation   | Choose a descriptive abbreviation. E.g. DHLPAKET_BLATT       |
| 2      | Name           | Choose a descriptive name. E.g. DHL Paket Blatt number range |
| 3      | Start value    | 1                                                            |
| 4      | Max. value     | 999                                                          |
| 5      | Auto. re-start | Activated                                                    |
| 6      | Leading zeros  | Activated                                                    |
| 7      | Char. length   | 3                                                            |

## Tracking no. type

### Identcode

No further data required.

### GS1 EAN 128 Licenseplate

![](https://files.readme.io/dcf87f87eac2a3cacdd22cc337059d6c133c523d32fe6babdeb1977cb9036ce1-image.png)

| Number | Field | Comment                                          |
| :----- | :---- | :----------------------------------------------- |
| 1      | GLN   | The GS1 base number of your company (7-9 digits) |

<br />

# EDI setups

In this section the EDI upload parameters are configured.

<Image align="center" src="https://files.readme.io/c3283f3a3a2cd0465245abf3b9abeb10162c31e8f782c9107481b09eb5d3ed07-edi.png" />

<br />

| Number | ID            | Comment                                                                                       |
| :----- | :------------ | :-------------------------------------------------------------------------------------------- |
| 1      | STANDARD      | This will send the standard EDI (when closing the pickup)                                     |
| 2      | PAPERLESS_COD | Only needed if you use the value added service **Paperless cash on delivery (DHLPAKETPLCOD)** |

Select the EDI ID you want to configure and click on _Open_.

![](https://files.readme.io/a4c145eec2a59f415d2db6a0c15752fa9136d5198eb9b9f158b1cf0d3f0eb1ef-image.png)

| Number | Field          | Comment                                                                                                                                                                  |
| :----- | :------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1      | EDI no. range  | The EDI number range. See [EDI number range](https://transport-freight-management.docs.developers.aeb.com/docs/dhl-paket-germany-account-configuration#edi-number-range) |
| 2      | EDI connection | Select STANDARD_2025                                                                                                                                                     |

<br />

<CCOEDINumberRange />

<br />

| Number | Field          | Comment                                                    |
| :----- | :------------- | :--------------------------------------------------------- |
| 1      | Abbreviation   | Choose a descriptive abbreviation. E.g. DHLPAKET_EDI       |
| 2      | Name           | Choose a descriptive name. E.g. DHL Paket EDI number range |
| 3      | Start value    | 1                                                          |
| 4      | Max. value     | 999                                                        |
| 5      | Auto. re-start | Activated                                                  |
| 6      | Leading zeros  | Activated                                                  |
| 7      | Char. length   | 3                                                          |

<br />
