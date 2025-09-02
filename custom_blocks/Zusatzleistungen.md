---
name: Zusatzleistungen
---
# Value-added services

<Callout icon="💡" theme="default">
  ### German: Zusatzleistungen
</Callout>

Value-added services are additional services, that can be combined with the typical service products of each carrier. These are often related to additional costs with the carrier, for specific information please check with your carrier person of contact.

<Image alt="Example of some value added services of UPS EMEA" align="center" src="https://files.readme.io/104b6fb-image.png">
  Example of some value-added services of UPS EMEA
</Image>

```json

"shipment": {
  "valueAddedServices": [
    {
      "identCode": "RETURNSERVICEALP"
    }
  ],
  ...
}
  
```
```xml
<shipment>
  <valueAddedServices>
      <identCode>RETURNSERVICEALP</identCode>
  </valueAddedServices>
  ...
</shipment>
```

To use these value-added services, there is one fields to be filled:

* `identCode`: Code of the value added service - available in the carrier configuration (ID next to the name).  

In order to be able to use the value-added service, it has to be enabled in the carrier configuration (indicated by the green checkmark in the carrier configuration).

![](https://files.readme.io/147488f-image.png)
