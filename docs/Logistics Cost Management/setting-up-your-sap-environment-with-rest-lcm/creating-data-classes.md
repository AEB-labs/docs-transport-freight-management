---
title: Creating data classes
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: setting-up-the-rest-call-class
      title: Setting up the REST call class
---
The data classes will define our fields per method and will be converted to a JSON structure later. There is a sub record structure that will be used by more than one interface.

## Generic subrecord

```Text Subrecord
CLASS zlcm_subrecords DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.

    TYPES:
      BEGIN OF zlcm_name_type_value,
        name  TYPE string,
        type  TYPE string,
        value TYPE string,
      END OF zlcm_name_type_value .
    TYPES:
      BEGIN OF zlcm_record,
        fields     TYPE TABLE OF zlcm_name_type_value WITH DEFAULT KEY,
        subrecords TYPE STANDARD TABLE OF REF TO zlcm_subrecords WITH DEFAULT KEY,
      END OF zlcm_record .

    DATA name TYPE string .
    DATA record TYPE zlcm_record .
*    DATA record TYPE REF TO zlcm_record .
protected section.
private section.
ENDCLASS.



CLASS ZLCM_SUBRECORDS IMPLEMENTATION.
ENDCLASS.
```

## Create service item 

```Text Create service item
CLASS zlcm_create_item_request DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.

    TYPES:
      BEGIN OF zlcm_company,
        company_number     TYPE string,
        name               TYPE string,
        street             TYPE string,
        postcode           TYPE string,
        city               TYPE string,
        country_i_s_o_code TYPE string,
      END OF zlcm_company .
    TYPES:
      BEGIN OF zlcm_date,
        date_in_timezone TYPE string,
        timezone         TYPE string,
      END OF zlcm_date .
    TYPES:
      BEGIN OF zlcm_value_unit,
        value TYPE string,
        unit  TYPE string,
      END OF zlcm_value_unit .
    TYPES:
      BEGIN OF zlcm_name_type_value,
        name  TYPE string,
        type  TYPE string,
        value TYPE string,
      END OF zlcm_name_type_value .
    TYPES:
      BEGIN OF zlcm_extendeddata,
        fields     TYPE TABLE OF zlcm_name_type_value WITH DEFAULT KEY,
        subrecords TYPE TABLE OF REF TO zlcm_subrecords WITH DEFAULT KEY,
      END OF zlcm_extendeddata .
    TYPES:
      BEGIN OF zlcm_item,
        item_id             TYPE string,
        scenario_ident_code TYPE string,
        service_ident_code  TYPE string,
        reference_number    TYPE string,
        order_number        TYPE string,
        service_provider    TYPE zlcm_company,
        orderer             TYPE zlcm_company,
        payer               TYPE zlcm_company,
        beneficiary         TYPE zlcm_company,
        reference_date      TYPE zlcm_date,
        pricing_date        TYPE zlcm_date,
        charge_date         TYPE zlcm_date,
        service_date        TYPE zlcm_date,
        order_date          TYPE zlcm_date,
        quantity            TYPE zlcm_value_unit,
        description         TYPE string,
        extended_data       TYPE zlcm_extendeddata,
      END OF zlcm_item .
    TYPES:
      BEGIN OF zlcm_parms,
        calculate_price_immediately    TYPE string,
        create_settlements_immediately TYPE string,
        return_trace_info              TYPE string,
        rollback_on_error_message      TYPE string,
      END OF zlcm_parms .

    DATA client_system_id          TYPE string .
    DATA client_ident_code         TYPE string .
    DATA user_name                 TYPE string .
    DATA result_language_iso_codes TYPE TABLE OF /aeb/01_char2 WITH DEFAULT KEY .
    DATA parms                     TYPE zlcm_parms .
    DATA items                     TYPE TABLE OF zlcm_item WITH DEFAULT KEY .
protected section.
private section.
ENDCLASS.



CLASS ZLCM_CREATE_ITEM_REQUEST IMPLEMENTATION.
ENDCLASS.
```

## Cancel service item

```
CLASS zlcm_cancel_item_request DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.

    TYPES:
      BEGIN OF item,
        item_id TYPE string,
      END OF item.

    DATA client_system_id TYPE string .
    DATA client_ident_code TYPE string .
    DATA user_name TYPE string .
    DATA reason_of_reversal TYPE string .
    DATA:
    resultlanguage_iso_codes TYPE TABLE OF /aeb/01_char2 WITH DEFAULT KEY .
    DATA:
      items TYPE TABLE OF item WITH DEFAULT KEY .

  PROTECTED SECTION.
  PRIVATE SECTION.

ENDCLASS.



CLASS ZLCM_CANCEL_ITEM_REQUEST IMPLEMENTATION.
ENDCLASS.
```