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

## Package number range

<Image border={false} src="https://files.readme.io/16f7817577364f09f3094a13e3c935ebb407545b025a0a0ae4c8a2080b775eda-image.png" />

| Field             | Comment                 | Start value | Max. value | Char. length | Leading zeros | Auto. re-start |
| :---------------- | :---------------------- | :---------- | :--------- | :----------- | :------------ | :------------- |
| Package no. range | Assigned by the carrier | 1           | 999999999  | 9            | Activated     | Activated      |

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

## EDI number range

For the EDI number range, you will need the UPS book numbers, which you will get from UPS.

|               |                         | Start value          | Max. value           | Char. length | Leading zeros | Auto. re-start |
| :------------ | :---------------------- | :------------------- | :------------------- | :----------- | :------------ | :------------- |
| EDI no. range | Assigned by the carrier | book number 1 + "01" | book number 2 + "99" | 9            | Activated     | Activate       |

Example:

* <br />

## Test environment

In the **test environment** you don't have to change anything:

<Image border={false} src="https://files.readme.io/966342c2689ad6275a6b2a2f347072978e3028a8e59c86b495bd040e77c1b39f-image.png" />

## Productive environment

In the **productive environment** you have to use your customer specific user and password, which you receive from UPS. You also need to use a different URL:

```Text URL
https://www.ha.ups.com/hapld/tos/kdwhapltos
```

<Image border={false} src="https://files.readme.io/f5ad378362f9da8647a4eb88e1d4e31d43634c5863cd3f7e61fc393703df1ac2-image.png" />

<br />

<br />

## Mapping: Terms of Delivery & Packages

* [Converting terms of delivery](https://rz3.aeb.de/docudata/OnlineHelp/cai/en-US/index.html#338067211620280459)
* [Converting package types](https://rz3.aeb.de/docudata/OnlineHelp/cai/en-US/index.html#338084491620282891)

<SinglePackageHandling />
