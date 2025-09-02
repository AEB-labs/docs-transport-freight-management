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
> ❗️ 
> 
> World Ease is not available for shipments between EU countries

# Requirements

UPS will provide a customer specific POE (Port of Entry) file to you, the customer, which you have to provide to AEB in order to import it into Carrier Connect. With this file UPS determines which shipments can be consolidated together. 

A shipment which will be consolidated is called a **child** shipment. The shipment containing these children is called **master** shipment.

There are specific requirements that shipments must meet to be consolidated:

## Requirements all shipments

:white_check_mark: All shipments (master and child) must have the same shipping date  
:white_check_mark: All shipments must have the same billing option

## Requirements master shipment

:white_check_mark: The importer must be entered in the master shipment as the recipient. This is done automatically when creating the master shipment from the first child shipment, provided that the importer is filled in the child.  
:white_check_mark: The master shipment must be a document shipment  
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

:x: Dangerous Goods  
:x: All UPS Return Services  
:x: UPS package types: Letter, 10KG BOX and 25KG BOX are not allowed in child shipments.  
:x: Document shipments are not allowed for child shipments

# Possible variants for World Ease shipments

## Variant 1: UPS World Ease – with DocBox

![](https://files.readme.io/ad9209cd53495faf4c6998f4629b7d049771f6d27e0cc017dc37f1dcacca6424-image.png)

<br />

## Variant 2: UPS World Ease – Paperless Invoice with DocBox

## Variant 3: UPS World Ease – Paperless Invoice without DocBox

<br />

# World Ease in connection with Trade document upload