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

## Customer data

<Image border={false} src="https://files.readme.io/a73f400873e88050390ab874a243744feb53246f5cf9d3fcd086c99f65b10f32-image.png" />

<br />

| Number | Field             | Comment                                                                                                                                     |
| :----- | :---------------- | :------------------------------------------------------------------------------------------------------------------------------------------ |
| 1      | Shipper           | The address of the shipper                                                                                                                  |
| 2      | Carrier address   |                                                                                                                                             |
| 3      | Customer number   | Assigned by the carrier                                                                                                                     |
| 4      | Depot number      | Assigned by the carrier                                                                                                                     |
| 5      | Package no. range | see [number ranges](https://transport-freight-management.docs.developers.aeb.com/docs/copy-of-ups-emea-carrier-configuration#number-ranges) |

## Number ranges

<CCONumberRanges />

### Package number range

<Image border={false} src="https://files.readme.io/3e4184a50459e8686cbb74751e61605a8494f877c993943d3eae0ffeab36a616-image.png" />

<Image border={false} src="https://files.readme.io/960d508e7eb5dd4ab7800a006ebc2704b67c83b3cae3f7b01736278d51040e3c-image.png" />

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

* Book-Nr. 1: 1234567 -> Start value: 123456701
* Book-Nr. 2: 1234568 -> Max. value: 123456899

## PLD upload

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
