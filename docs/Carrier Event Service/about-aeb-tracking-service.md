---
title: About Carrier Event Service
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
Thank you for your interest in our Carrier Event Service API. We would like to make it as easy as possible for you to get started using the Carrier Event Service. Please feel free to contact us if you miss information or if you find a way to make it even easier.

Let's start with the business object model of the Carrier Event Service. In the business object model, the connection between Carrier Connect and the Carrier Event Service is clarified. You already know the business objects **shipment** and **package** from the Carrier Connect business object model.

The Carrier Event Service adds the **tracking object** and the **carrier event** to the business object model. Each shipment has at least one tracking object. A tracking object either belongs to a shipment or to a package. If each package in the shipment can be tracked individually, the tracking object is a trackable package. If only the shipment can be tracked and not the individual packages, the tracking object is a trackable shipment. 

![775](https://files.readme.io/8ecea65-CES_Datenmodell2.png "CES_Datenmodell2.png")

The carrier events represent the tracking data provided by the carriers in a standardized format. They can be assigned to either one or no tracking object. Each carrier event contains, among other things, the standardized ident code of the event as well as the original ident code provided by the carrier.
