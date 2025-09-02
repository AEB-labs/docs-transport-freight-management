---
title: Carrier, Service, Value-Added Service and Info Text Identifiers
excerpt: >-
  In this section you will learn where to find the correct identifiers for
  carriers, services, value-added services and info texts.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
[block:html]
{
  "html": "<style>\n  span.cm-s-neo {\n    background-color: #f2f2f2;\n    color: red;\n  }\n</style>"
}
[/block]


# Carrier Identifiers: carrierIdentCode

```json
"shipment": {
    "...":"...",
    "carrierIdentCode": "UPS",
}
```
```xml
<shipment>
  <...></...>
  <carrierIdentCode>UPS</carrierIdentCode>
</shipment>
```

Each carrier is assigned a unique code within Carrier Connect. You can find the _carrierIdentCode_ in Carrier Connect under **Master data > Carrier configurations** in the column **ID**:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/540f1e27d8720380c610fcb1b84b8cd6f8fb47acf6dd4c16e3ea01d491dac48e-image.png",
        null,
        "carrierIdentCode"
      ],
      "align": "center"
    }
  ]
}
[/block]


# Service Identifiers: serviceCode

```json
"shipment": {
    "...":"...",
    "serviceCode": "UPS_EXPR",
}
```
```xml
<shipment>
  <...></...>
  <serviceCode>UPS_EXPR</serviceCode>
</shipment>
```

Services offered by carriers, such as express delivery or standard shipping, have specific codes. In Carrier Connect go to **Master data > Carrier configurations**. Open the desired carrier and chose the tab **Services**. You can find the _serviceCode_ in the column **ID**:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9ba3e534aa24983b0055957fddc29991b856c8e01c59ae59d5261f1056fcee8d-image.png",
        null,
        "serviceCode"
      ],
      "align": "center"
    }
  ]
}
[/block]


# Value-Added Service Identifiers: valueAddedServices

```json
"shipment": {
    "...":"...",
    "valueAddedServices": [
      {
        "identCode": "COD"
      }
    ]
}
```
```xml
<shipment>
  <...></...>
  <valueAddedServices>
    <identCode>COD</identCode>
  </valueAddedServices>
</shipment>
```

Additional services, like saturday delivery or a return service, are also identified by unique codes. In Carrier Connect go to **Master data > Carrier configurations**. Open the relevant carrier and chose the tab **Value-added services**. You can find the right _identCode_ in the column **ID**:

![](https://files.readme.io/d0b1a481befa7bacfbc48b877c75d1387fd57764cba5887e6dba181c4cc183ec-image.png)

# Info Text Identifiers: carrierInfoTexts

```json
"shipment": {
    "...":"...",
    "carrierInfoTexts": [
      {
        "identCode": "00",
        "parameter": "some info for the carrier" //only necessary if Additional info = Required.
      }
    ]
}
```
```xml
<shipment>
  <...></...>
  <carrierInfoTexts>
    <identCode>00</identCode>
    <parameter>some info for the carrier</parameter> //only necessary if Additional info = Required.
  </carrierInfoTexts>
</shipment>
```

The _identCode_ for an info text specifies which predefined message will be sent to the carrier.

In Carrier Connect go to **Master data > Carrier configurations**. Open the relevant carrier and chose the tab **Info texts**. You can find the right _identCode_ in the column **Name**:

> ❗️ Important
> 
> Use only the part before the hyphen.
> 
> **Example:**  
> For `00 - General comment:`, use `00` as the _identCode_.

If additional information is needed, enter it in the _parameter_ field.

![](https://files.readme.io/22e642f64efe857c87d9730ee03276376f90e0892f4937b00ebb1fe41f0b10af-image.png)