---
title: Loading Dock Scheduling Objects
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
## Overview

<Image width="smart" src="https://files.readme.io/33bff3c-Draw-io_lds_objects.png" />

## Loading Location

A Loading location represents a physical location, e.g. a warehouse, that has one or more loading ramps at which vehicles can dock to load and unload materials.

Some information a Loading Location can contain:

* Location specific Settings
  * Default time slot length
  * Lead time
  * ...
* Holiday calendar
* Address

## Loading Ramp

A loading ramp always belongs to a specific Loading Location. It represents a loading ramp at which vehicles can dock to load or unload.\
Time slots are used to indicate that a loading ramp is occupied by a vehicle.

Some information a Loading Ramp can contain:

* Ramp type (Loading, Unloading, Loading & Unloading)

## Loading Order

A Loading Order is used to represent an order that needs to be processed at a loading ramp.\
It contains information about the transport that needs to be processed, such as:

* Loading Type (Loading, Unloading, Loading & Unloading)
* License plate number
* Driver contact info
* Forwarder
* Loaded items
* Documents

## Time Slot

A Time Slot is the time period of time at a specific loading ramp at which the connected loading order is processed.

It can contain the following information:

* Loading Order for which the time slot is booked
* Loading Ramp at which the time slot is booked
* Preparation time
* Post processing time
* Planned arrival / departure
* Actual arrival / departure
