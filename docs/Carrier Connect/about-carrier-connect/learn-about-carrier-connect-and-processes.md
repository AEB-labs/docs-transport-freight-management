---
title: Basic features and processes
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
# What is Carrier Connect?

The multi-carrier platform *Carrier Connect* lets you send single- and multi-package shipments around the\
world with international carriers and parcel services.

<Callout icon="🔎" theme="default">
  ### System description Carrier Connect

  Detailed information can be found in the section 2 of the <a href="https://docs.aeb.com/doc/cm-287951243-801476363-en-US/t-801476363-780627851-en-US" target="_blank">System decription of Carrier Connect API</a>.
</Callout>

# Process and basic features at a glance

<Image align="center" src="https://files.readme.io/4533de9-CCO-Prozess_en.png" />

## Transfer shipping order data from the host system

You can transfer shipping order data from your host system using the web service interface or enter this\
data manually right in the *Carrier Connect* user interface. The shipping order data includes all the\
information needed to process a shipment: consignor and consignee address, package and item data,\
carrier, shipping options, etc.

## Generate and prepare shipping labels and documents

*Carrier Connect* provides the correct shipping label and any other shipping documents, then feeds them\
back to your host system so that they can be shared with the selected printer. If it’s not possible to\
prepare the label correctly, you have the option to print an error label with the error message instead of\
the shipping label. As soon as the labels have been prepared, the host system can access the tracking\
numbers in order to track the package and shipment. The *Carrier Event Service* option gives you access\
to your carriers' tracking data.

## Generate and complete pickup

When shipping orders are completed, they are consolidated into pickups. The shipping orders to be\
consolidated can be selected either automatically using rule-based pickup strategies or manually. When\
the pickup is complete, the configured documents, e.g. manifests are generated in PDF format and\
shared via API with the host system.

## Transmit shipping order data to carrier

At the same time the pickup is completed, the shipping order data is transmitted to the carrier either as a\
file upload (EDI) or through a web service interface (sometimes even while the label is being generated).
