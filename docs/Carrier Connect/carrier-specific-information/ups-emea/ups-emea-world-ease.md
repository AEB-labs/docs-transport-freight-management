---
title: 'UPS EMEA: Collective Customs Clearance: UPS World Ease'
excerpt: >-
  UPS World Ease allows multiple shipments destined for one country to be
  consolidated into a single consolidated shipment. In this case, a consolidated
  shipment is cleared by an appointed importer in the receiving country, who is
  responsible for paying duties and taxes. Where goods destined for one or more
  locations within the EU are to be exported from a third country, UPS can
  simplify the process by arranging for an EU country to serve as the point of
  entry.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
<Callout icon="❗️" theme="error">
  World Ease is not available for shipments between EU countries
</Callout>

# Requirements

UPS will provide a customer specific POE (Port of Entry) file to you, the customer, which you have to provide to AEB in order to import it into Carrier Connect. With this file UPS determines which shipments can be consolidated together.

A shipment which will be consolidated is called a **child** shipment. The shipment containing these children is called **master** shipment.

There are specific requirements that shipments must meet to be consolidated:

## Requirements all shipments

:white_check_mark: All shipments (master and child) must have the same shipping date

:white_check_mark: All shipments must have the same billing option

## Requirements master shipment

:white_check_mark: The importer must be entered in the master shipment as the recipient. This is done automatically when creating the master shipment from the first child shipment, provided that the importer is filled in the child.

:white_check_mark: The master shipment must be a document shipment (is done automatically by Carrier Connect)

:white_check_mark: A maximum of one package is allowed in the master shipment

:white_check_mark: The value added service _World Ease® Master_ must be set in the master shipment

## Requirements child shipment

:white_check_mark: All child shipments must use the same clearance port as the master-shipment

:white_check_mark: All child shipments must use the same importer

:white_check_mark: All child shipments must be goods shipments

:white_check_mark: The currency for all child shipments must be identical, e.g. EUR everywhere

:white_check_mark: The unit of weight for all child shipments must be identical. As of 08/2019 only KGS is implemented

:white_check_mark: All child shipments within a master shipment for UPS Expedited and UPS Standard (Package and Shipment) **must contain the same service level**. UPS Express, UPS Epress Plus and UPS Express Saver are allowed within one World Ease shipment. The allowed service level can be seen in the POE file.

:white_check_mark: The value added service _World Ease® Child_ must be set in the child shipment

## Not allowed for World Ease

:x: All UPS Return Services

:x: UPS package types: Letter, 10KG BOX and 25KG BOX are not allowed in child shipments.

:x: Document shipments are not allowed for child shipments

## World Ease in connection with Trade document upload

The value added service "Trade document upload" can be used in combination with World Ease, but only in combination with Paperless Invoice, i.e. variant 2 and variant 3, see below. This excludes an upload of the commercial invoice. The upload of documents is only possible in the child shipments, not in the master shipment.

The upload of documents for collective customs clearance is not provided by UPS in combination with World Ease or as an exception only in a special process which requires an internal approval procedure. UPS assumes that the customs relevant data will normally be uploaded via EDI and that the customer will provide a blank letterhead on which (upon request) a printout can be made as a customs invoice. As a rule, however, this is all handled electronically.

# Possible options for World Ease shipments

## Option 1: UPS World Ease – with DocBox

Master-shipment contains shipment documents.

* Master-shipment specification:  1 package with dimensions L/W/H each 1 cm, weight 1 kg must be created. Set UPS "02 - customer's own packaging" for package conversion  . This package represents the green document box containing the transport documents for World Ease shipments.
* A label is printed for each package in the child-shipment and for the package in the master-shipment
* For the master-shipment, the MasterInvoice document and the CID are also printed.
* Value added service "Paperless Invoice" and "Paperless Invoice (additional documents) are in Master- and Child-Shipment not allowed

❌ Please note "Trade document upload" not possible with this variant!

![](https://files.readme.io/ad9209cd53495faf4c6998f4629b7d049771f6d27e0cc017dc37f1dcacca6424-image.png)

<br />

## Option 2: UPS World Ease – Paperless Invoice with DocBox

Master-shipment with Paperless Invoice and shipment documents.

* Master shipment specification:  1 package with dimensions L/W/H 1 cm each, weight 1 kg must be created
  This package represents the green document box containing the transport documents for World Ease shipments
* Child-shipment specification:  Paperless Invoice (additional documents) must be activated in each child shipment
* A label is printed for each package in the child-shipment and for the package in the master-shipment
* For the master-shipment the document MasterInvoice and the CID will be printed additionally

## Option 3: UPS World Ease – Paperless Invoice without DocBox

Master shipment with Paperless Invoice without shipment documents.

* Master-Shipment specification:  : There is no package, a virtual package is generated in the shipment
* Child shipment specification:  Paperless Invoice must be activated in each child shipment
* A label is printed for each package in the child-shipment
* For the master-shipment the SummaryLabel is printed, which should be stuck on the last package
* Neither MasterInvoice nor CID are printed for the master-shipment

![](https://files.readme.io/a06acb83d8bd1f6d43bee5802504cca1a02f2dc8b0502e15228f487bb1610e22-image.png)

<br />

<br />
