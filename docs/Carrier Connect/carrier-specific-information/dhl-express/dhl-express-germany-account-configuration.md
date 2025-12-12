---
title: 'DHL Express (Germany): Account Configuration'
deprecated: false
hidden: true
metadata:
  robots: index
---
<CCOConfiguringCarriersInCarrierConnect />

To create a new DHL Express account in Carrier Connect, open DHL Express in _Master data > Carrier configurations_. In the tab _Accounts_ click on _New_.

Select account type

* (1) DHLEXPINT_MYDHLAPIV2 **only** if you will use the value-added service **Pickup Booking** (DHLEXPINTPICKUP).
* (2) DHLEXPINT_STD_IFTMIN in all other cases.

<Image align="center" border={false} src="https://files.readme.io/d796c2931115232843a976fab7f56f06983c041e2470fe02c8d686d6cabfbd4a-account-type.png" />

# DHL Express account

## (2) Account type: DHLEXPINT_STD_IFTMIN

<Image align="center" border={false} src="https://files.readme.io/38e2cd3d9a17b218a89586718831aa511d10b54452740bb07ebf571e7bc18b85-account1.png" />

<Image align="center" border={false} src="https://files.readme.io/656817ad7043b2882ef9b62c7b653cdac21dc110bce4ae8d0901dc7418314ff5-account2.png" />

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
        See below: **Single Package Handling**
      </td>
    </tr>

    <tr>
      <td>
        5
      </td>

      <td>
        Export Customer no.
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
        Shipper IATA code
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
        Participation no.
      </td>

      <td>
        Assigned by the carrier
      </td>
    </tr>

    <tr>
      <td>
        8
      </td>

      <td>
        AWB no. range
      </td>

      <td>
        See [AWB no. range](https://transport-freight-management.docs.developers.aeb.com/docs/dhl-express-germany-account-configuration#awb-no-range)
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
        Set to _Send and log_.
      </td>
    </tr>

    <tr>
      <td>
        10
      </td>

      <td>
        Document upload
      </td>

      <td>
        If you need to transmit documents electronically to DHL, set to _Send and log_.
      </td>
    </tr>

    <tr>
      <td>
        11
      </td>

      <td>
        License plate type
      </td>

      <td>
        Assigned by the carrier. There are two options:

        * ASC MH 10
        * GS1-128 (SSCC)

        See [License plate type](https://transport-freight-management.docs.developers.aeb.com/docs/dhl-express-germany-account-configuration#license-plate-type)
      </td>
    </tr>

    <tr>
      <td>
        12
      </td>

      <td>
        License pl. no. range
      </td>

      <td>
        See [License pl. no. range](https://transport-freight-management.docs.developers.aeb.com/docs/dhl-express-germany-account-configuration#license-pl-no-range-1)
      </td>
    </tr>
  </tbody>
</Table>

<CCOSinglePackageHandling />

<br />

<CCOPackageNumberRange />

### AWB no. range

| Number | Field          | Comment                                                          |
| :----- | :------------- | :--------------------------------------------------------------- |
| 1      | Abbreviation   | Choose a descriptive abbreviation. E.g. DHLFREIGHT_PCK           |
| 2      | Name           | Choose a descriptive name. E.g. DHL Freight package number range |
| 3      | Start value    | 1                                                                |
| 4      | Max. value     | 999999999                                                        |
| 5      | Auto. re-start | Activated                                                        |
| 6      | Leading zeros  | Activated                                                        |
| 7      | Char. length   | 9                                                                |

### License pl. no. range

| Number | Field          | Comment                                                          |
| :----- | :------------- | :--------------------------------------------------------------- |
| 1      | Abbreviation   | Choose a descriptive abbreviation. E.g. DHLFREIGHT_PCK           |
| 2      | Name           | Choose a descriptive name. E.g. DHL Freight package number range |
| 3      | Start value    | 1                                                                |
| 4      | Max. value     | 999999999                                                        |
| 5      | Auto. re-start | Activated                                                        |
| 6      | Leading zeros  | Activated                                                        |
| 7      | Char. length   | 9                                                                |

## License plate type

### ASC MH 10

<Image align="center" border={false} src="https://files.readme.io/d14368ff232e5fad8e0051d98ae474e7a07a21c470b64b176042d3a4468c0d2c-lp.png" />

| Number | Field     | Comment                 |
| :----- | :-------- | :---------------------- |
| 1      | ASC MH 10 | Assigned by the carrier |

### GS1-128 (SSCC)

<Image align="center" border={false} src="https://files.readme.io/95d4b0311bac746ef9afc0412ec1e15f4e59eba51a5ce934ac216a13704da115-gs1.png" />

| Number | Field | Comment                                          |
| :----- | :---- | :----------------------------------------------- |
| 1      | GLN   | The GS1 base number of your company (7-9 digits) |

<br />

## Return services

You will need a second customer number and a second package number range, if you are using one of the DHL Express return services:

* Data staging – return (enclosed) (DHLEXPINTRETURN)
* Data staging - Return (on demand) (DHLEXPINTRETURNOD)

<Image align="center" border={false} src="https://files.readme.io/a0735ceae6e92372d6c64bc9e9958fb605c7139ec8112c42d24089f9b9f1163d-return-services.png" />

| Number | Field               | Comment                                                                                                                                                                                                                                   |
| :----- | :------------------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1      | Import Customer no. | Assigned by the carrier                                                                                                                                                                                                                   |
| 2      | Return pack. range  | A second package number range assigned by the carrier. It's configured like the [package number range](https://transport-freight-management.docs.developers.aeb.com/docs/dhl-express-germany-account-configuration#package-number-range). |

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
