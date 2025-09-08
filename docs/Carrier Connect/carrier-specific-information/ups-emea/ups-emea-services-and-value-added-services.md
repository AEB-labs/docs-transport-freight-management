---
title: 'UPS EMEA: Services and Value Added Services'
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
# Services

## Service UPS Access Point™ Economy

The UPS Access Point™ Economy service is a slower, more economical alternative to the UPS Standard domestic service and is available for domestic shipments in Belgium, Canada, France, Germany, Italy, Luxembourg, Mexico, Netherlands, Poland, United Kingdom, and satellites of these countries.

> ❗️
>
> Must be combined with:
>
> * Access Point™ – Ship to a UPS Access Point™ Location
> * Access Point™ – Electronic authorization code
> * Access Point™ – Addressee Only Delivery
> * Access Point™ – C.O.D
>
> Must not be combined with:
>
> * Access Point™ – Not at home UPS Access Point™ delivery

# Value Added Services

## UPS Access Point options

For shipments specifically to, from or between UPS Access Point locations. 

A shop delivery ID needs to be filled in order to make sure that shipment is delivered to the correct access point location.

![](https://files.readme.io/8dc61c7a4be53d9f0cef4c162bf5aac9b4d4f613d3b4862f60005914f6c0dba9-image.png)

<br />

There are 2 options to fill the Shop Delivery ID of the acccess point (for either pickup or delivery): 

a) ShopID  of the UPS Access Point location is filled by you via the interface or manually directly in the field Serv. pt. ID pickup or Serv. pt. ID delivery. Based on this, the corresponding address is determined via the Webservice Locator API and entered automatically in the shipping order.

OR

b) If the ShopID of the UPS Access Point location is not filled in Carrier Connect, the closest access point will be  determined via the Webservice Locator API during label printing and entered automatically in the shipping order in the folder "Extended information" in the field Serv. pt. ID pickup or Serv. pt. ID delivery. The corresponding address of the UPS Access Point location found is entered behind it.

<br />

### Access Point - Addressee Only Delivery

With this service, you enable your customers to ensure that only the original consignee named on the shipping label may collect the parcel from the UPS Access Point location (no pick-up by a third party allowed).

> ❗️
>
> Must be combined with:
>
> * Access Point™ – Ship to a UPS Access Point™ Location
>
> Must not be combined with:
>
> * Access Point™ – Electronic authorization code

<br />

### Access Point - C.O.D

Collect on delivery collected at the UPS Access Point ™. 

> ❗️
>
> Must be combined with:
>
> Access Point™ – Ship to a UPS Access Point™ Location

<br />

### Access Point - Not at home UPS Access Point delivery

Delivery to a UPS Access Point (after the first, unsuccessful delivery attempts). UPS InfoNotice is stored, informing customers that and where they can collect their parcels

> ❗️
>
> May not be combined with the other Access Point value-added services

### Access Point - Electronic authorization code

Electronic authorization code for package pickup.

Provide your customers with a security code. This give them more security and also enable them to have their parcels collected by a third party. This option also allows the use of the UPS Access Point network if the identity of the recipient is unknown (e.g. customer service technician). The authorization code is entered in the extra field "Electronic authorization code - UPSELAUTHCODE" 

> ❗️
>
> Must be combined with:
>
> Access Point™ – Ship to a UPS Access Point™ Location
>
> Must not be combined with:
>
> Access Point™ – Addressee Only Delivery

<br />

### Access Point - Ship to a UPS Access Point Location

This topic describes the UPS Access Point™ pick-up service, which offers consumers an alternative to home delivery. Shipments are delivered directly to UPS Access Point™ locations where customers can pick up their packages. UPS Access Point™ locations are retail locations that facilitate transactions on behalf of UPS.

> ❗️
>
> Can be combined with:
>
> Access Point™ – Electronic authorization code\
> Access Point™ – Addressee Only Delivery\
> Access Point™ – C.O.D

<br />

## Documentupload - Trade document upload

For further information see helpcenter article [UPS: Digitally transmitting commercial invoices and customs documents to UPS via Carrier Connect](https://service.aeb.com/hc/en-us/articles/21092474921489-UPS-Digitally-transmitting-commercial-invoices-and-customs-documents-to-UPS-via-Carrier-Connect)

## Paperless Invoice

For further information see helpcenter article [UPS: Digitally transmitting commercial invoices and customs documents to UPS via Carrier Connect](https://service.aeb.com/hc/en-us/articles/21092474921489-UPS-Digitally-transmitting-commercial-invoices-and-customs-documents-to-UPS-via-Carrier-Connect)

## Return Services

All options have in common that UPS does not proactively drive to the customer to pick up a provided package but waits for the customer to contact UPS. UPS then reactively sends a driver to pick up the package.

> ❗️
>
> We currrently only implemented on demand return services meaning you need to create an additional shipping order for the return shipment - with new reference number.

### Return Service – Electronic Return Label

You have the option to provide your customers in over 135 countries with a return shipping label via email. Your customer can print this label and the control document or drop off the package at an authorized UPS shipping location before contacting UPS to arrange a pickup.

As soon as a corresponding EDI has been transmitted to UPS, UPS generates a shipping label on its own servers which is sent to the collection customer by e-mail for self-printing. Therefore, in this case, the e-mail address of the collection customer is mandatory, i.e. to fill in Carrier Connect.

### Return Service – Print Return Label

With the "Return Service - Print Return Label (Self print)", you can print the return label yourself and include it with outgoing shipments to over 135 countries. You can also send the label separately to your customer after shipping the package separately. Customers then simply affix the label to their package or drop off the package at an authorized UPS shipping location and contact UPS for a pickup.

When transferring to Carrier Connect, the user gets back a label, which he then saves e.g. via PDF print in a directory or manually attaches to an email.

Beware: We only implemented this option as a on demand return service. Hence, you need to create an additional shipping order only for the return shipment.

### Return Service – One Attempt

With this service you can order a pickup for immediate return of a package. The UPS driver will make an attempt to pick up the package. If the driver does not meet the customer at the "UPS Return Service - One Attempt", he leaves the sticker with the customer, who then simply affixes it to the package and either takes it to a UPS drop-off point or contacts UPS for collection.

No label is generated during the transfer to Carrier Connect. The EDI transfer counts as an order for UPS. The UPS driver brings a label to the customer and attaches it to the package there.

### Return Service – Three Attempt

With this service you can order a pickup for immediate return of a package. The UPS driver will make three attempts to pick up your shipment on three consecutive business days. If the driver still cannot pick up the shipment on the third attempt, the label will be returned to UPS.

No label is generated during the transfer to Carrier Connect. The EDI transmission counts as an assignment for UPS. The UPS driver brings a label to the customer and attaches it to the package there.

### Return Service - Print & Mail - invalid as of Feature Pack 08/2022
