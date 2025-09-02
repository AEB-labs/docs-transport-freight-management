---
title: Get to know the Object Model
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
You have now a basic understanding of *Carrier Connect* – let's have a closer look at the objects the system uses. 

<Image align="center" src="https://files.readme.io/d146a7c86e8578e0386954cbc488f4e2452af1fffa9ac59dff105c02dd9ba889-Get_Started_Carrier_Connect_JWA_-_Object_Model.jpg" />

# Shipping order

**The data structures in the shipping order**:

* The "Head" describes the header data of the shipping order. Among other things, it contains information on the shipper and recipient of the shipment as well as information on the handling conditions.
* The "Packages" represent the packages to be shipped. They contain information such as the dimensions and weight.
* The "Items" describe the items shipped in the shipment. They contain information such as the value and quantity of each item. Items can be packed in packages. So the relationship between items and packages is n:m.
* The "Carrier and service" contains the selected shipping option for the shipment. The desired carrier is automatically derived from the selected service code and is returned as part of the response.

# Pickup

When shipping orders are completed, they are bundled into so-called pickups. When a pickup is complete, the configured documents, such as the manifest, are generated as a PDF and made available to the source system via API. At the same time as the pickup is completed, the shipping orders data is sent to the carrier via EDI or webservice.
