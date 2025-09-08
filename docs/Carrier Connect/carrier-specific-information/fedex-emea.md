---
title: FedEx EMEA
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Harardous Goods

## Lithium batteries

### IATA

createShipment

```json
{
  ...
  "shipment": {
    ...
    "items": [
      {
        "referenceNumber1": "1000-1",
        "description": "Item #1",
        ...
        "hazardousGoodsItems": [
          {
            "unNumber": "3481",
            "hazardRegulation": "IATA",
            "technicalName": "Lithium ion Batteries",
            "hazardClass": "9",
            "specialSubstanceType": "LITHIUM_BATTERY",
            "packingInstruction": "966_II",
            "hazardWeight": {
              "unit": "kg",
              "value": 1.0
            }
          }
        ]
      }
    ],
    "packages": [
      {
        "referenceNumber1": "10001",
        ...
        "hazardousGoodsData": {
          "hazardousGoodsType": "SPECIAL_SUBSTANCE"
        },
        "containedItems": [
          {
            "itemTransactionId": "1000-1",
            "referenceNumber1": "1000-1",
            "quantityValue": "15"
          }
        ]
      }
    ]
  }
}
```
