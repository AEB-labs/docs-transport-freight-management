---
title: 'DHL Freight (Germany): Carrier Configuration'
deprecated: false
hidden: false
metadata:
  robots: index
---
<CCOConfiguringCarriersInCarrierConnect />

# Account configuration

To create a new DHL Freight account in Carrier Connect, open DHL Freight in _Master data > Carrier configurations_. In the tab _Accounts_ click on _New_.

## Tab: DHL Freight account

<Image border={false} src="https://files.readme.io/a73f400873e88050390ab874a243744feb53246f5cf9d3fcd086c99f65b10f32-image.png" />

<Image border={false} src="https://files.readme.io/901975d59003b80e956aaa21237004bf160eb59f7607201b5d23a24e43423632-image.png" />

<br />

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
        see [Number ranges](https://transport-freight-management.docs.developers.aeb.com/docs/copy-of-ups-emea-carrier-configuration#number-ranges)
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

### Number ranges

<CCONumberRanges />

### Package number range

<br />

|                   |                         | Start value | Max. value | Char. length | Leading zeros | Auto. re-start |
| :---------------- | :---------------------- | :---------- | :--------- | :----------- | :------------ | :------------- |
| Package no. range | Assigned by the carrier | 4.000.000   | 7.999.999  | 7            | Activated     | Activated      |

<br />

### EDI number range

For the EDI number range, you will need the UPS book numbers, which you will get from UPS.

|               |                         | Start value          | Max. value           | Char. length | Leading zeros | Auto. re-start |
| :------------ | :---------------------- | :------------------- | :------------------- | :----------- | :------------ | :------------- |
| EDI no. range | Assigned by the carrier | book number 1 + "01" | book number 2 + "99" | 9            | Activated     | Activate       |

Example:

* <br />

### Tracking no. type

## EDI upload

In this section the EDI upload parameters are configured.

### Test environment

In the **test environment** you don't have to change anything:

<Image border={false} src="https://files.readme.io/966342c2689ad6275a6b2a2f347072978e3028a8e59c86b495bd040e77c1b39f-image.png" />

### Productive environment

In the **productive environment** you have to use your customer specific user and password, which you receive from UPS. You also need to use a different URL:

```Text URL
https://www.ha.ups.com/hapld/tos/kdwhapltos
```

<Image border={false} src="https://files.readme.io/f5ad378362f9da8647a4eb88e1d4e31d43634c5863cd3f7e61fc393703df1ac2-image.png" />

<br />

## Web service parameter

If you're shipping dangerous goods or use the value added service _Access Points_ or _Trade document upload_, you need to configure the section _Web service parameter_. For more infos see [here](https://transport-freight-management.docs.developers.aeb.com/docs/ups-emea#webservice-for-dangerous-goods-access-points-or-trade-document-upload).

<br />

<Image border={false} src="https://files.readme.io/d350d32707368134ea374256a41a7419e32ef41484c030bf2101c1367a6c78a6-image.png" />

<br />

<br />

## Mapping: Terms of Delivery & Packages

* [Converting terms of delivery](https://rz3.aeb.de/docudata/OnlineHelp/cai/en-US/index.html#338067211620280459)
* [Converting package types](https://rz3.aeb.de/docudata/OnlineHelp/cai/en-US/index.html#338084491620282891)

## Single Package Handling

* The package number and the total number of packages are usually printed on the package label, e.g. 1 OF 2 for the first package, 2 OF 2 for the second package. Exception is the UPS service "Standard Package". With this service, 1 OF 1 is always printed on each package label, regardless of how many packages there are in total.
* If single package handling is activated, 1 OF _, 2 OF _, etc. will be printed on the label for all services except "UPS Standard Package".
