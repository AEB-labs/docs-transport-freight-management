---
title: Program to create a service item
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
      slug: programm-to-cancel-a-service-item
      title: Program to cancel a service item
---
Please treat this program as example. You can integrate the call in your SAP system where it suits your process most.

```Text Create service item
*&---------------------------------------------------------------------*
*& Report ZSME_CREATE_LCM_SERVICE_ITEM
*&---------------------------------------------------------------------*
*&
*&---------------------------------------------------------------------*
REPORT zlcm_create_lcm_service_item.

DATA: lo_request      TYPE REF TO zlcm_create_item_request,
      ls_item         TYPE zlcm_create_item_request=>zlcm_item,
      ls_field        TYPE zlcm_create_item_request=>zlcm_name_type_value,
      lo_subrecord    TYPE REF TO zlcm_subrecords,
      lo_subsubrecord TYPE REF TO zlcm_subrecords,
      ls_record       TYPE zlcm_subrecords=>zlcm_record
      .

DATA(lo_zlcm_rest_call) = zlcm_rest_call=>new_for( im_destination = 'NAME' ).

create OBJECT lo_request.

lo_request->client_ident_code = 'CLIENT'.
lo_request->client_system_id = sy-sysid && '_' && sy-mandt.
lo_request->user_name = sy-uname.
APPEND 'de' TO lo_request->result_language_iso_codes.

lo_request->parms-create_settlements_immediately = 'false'.
lo_request->parms-calculate_price_immediately = 'false'.
lo_request->parms-return_trace_info = 'true'.

ls_item-item_id = '25-11-2022'.
ls_item-scenario_ident_code = 'FREIGHT'.
ls_item-service_ident_code = 'DHL_DOM_EXPR'.
ls_item-reference_number = '25-11-2022'.
ls_item-order_number = '25-11-2022'.

ls_item-service_provider-company_number = 'TNT'.
ls_item-service_provider-name = 'TNT Express Worldwide'.
ls_item-service_provider-street = 'Heilbronner Staße 110'.
ls_item-service_provider-postcode = '70334'.
ls_item-service_provider-city = 'Stuttgart'.
ls_item-service_provider-country_i_s_o_code = 'DE'.

ls_item-orderer-company_number = '001'.
ls_item-orderer-name = 'AEB SE'.
ls_item-orderer-street = 'Sigmaringer Straße 109'.
ls_item-orderer-postcode = '70567'.
ls_item-orderer-city = 'Stuttgart'.
ls_item-orderer-country_i_s_o_code = 'DE'.

ls_item-payer-company_number = '001'.
ls_item-payer-name = 'AEB SE'.
ls_item-payer-street = 'Sigmaringer Straße 109'.
ls_item-payer-postcode = '70567'.
ls_item-payer-city = 'Stuttgart'.
ls_item-payer-country_i_s_o_code = 'DE'.

ls_item-beneficiary-company_number = '001'.
ls_item-beneficiary-name = 'AEB SE'.
ls_item-beneficiary-street = 'Sigmaringer Straße 109'.
ls_item-beneficiary-postcode = '70567'.
ls_item-beneficiary-city = 'Stuttgart'.
ls_item-beneficiary-country_i_s_o_code = 'DE'.

ls_item-reference_date-date_in_timezone = '2022-11-25 12:00:00'.
ls_item-reference_date-timezone = 'Europe/Berlin'.

ls_item-pricing_date-date_in_timezone = '2022-11-25 12:00:00'.
ls_item-pricing_date-timezone = 'Europe/Berlin'.

ls_item-charge_date-date_in_timezone = '2022-11-25 12:00:00'.
ls_item-charge_date-timezone = 'Europe/Berlin'.

ls_item-service_date-date_in_timezone = '2022-11-25 12:00:00'.
ls_item-service_date-timezone = 'Europe/Berlin'.

ls_item-order_date-date_in_timezone = '2022-11-25 12:00:00'.
ls_item-order_date-timezone = 'Europe/Berlin'.

ls_item-quantity-value = '1'.
ls_item-quantity-unit = 'St'.

ls_item-description = 'Shipment'.

ls_field-name = 'carrierDefinitionIdentCode'.
ls_field-type = 'string'.
ls_field-value = 'TNT'.
APPEND ls_field TO ls_item-extended_data-fields.

ls_field-name = 'numberOfInvoices'.
ls_field-type = 'decimal'.
ls_field-value = '1'.
APPEND ls_field TO ls_item-extended_data-fields.

ls_field-name = 'isDangerousGoods'.
ls_field-type = 'boolean'.
ls_field-value = 'false'.
APPEND ls_field TO ls_item-extended_data-fields.

ls_field-name = 'referenceNumber'.
ls_field-type = 'string'.
ls_field-value = 'referenceNumber'.
APPEND ls_field TO ls_item-extended_data-fields.

ls_field-name = 'incotermIdentCode'.
ls_field-type = 'string'.
ls_field-value = 'incoterm'.
APPEND ls_field TO ls_item-extended_data-fields.

ls_field-name = 'numberOfItems'.
ls_field-type = 'decimal'.
ls_field-value = '2'.
APPEND ls_field TO ls_item-extended_data-fields.

ls_field-name = 'palletPlaces'.
ls_field-type = 'decimal'.
ls_field-value = '1.000'.
APPEND ls_field TO ls_item-extended_data-fields.

ls_field-name = 'numberOfPackages'.
ls_field-type = 'decimal'.
ls_field-value = '2'.
APPEND ls_field TO ls_item-extended_data-fields.

ls_field-name = 'isDocumentShipment'.
ls_field-type = 'boolean'.
ls_field-value = 'false'.
APPEND ls_field TO ls_item-extended_data-fields.

ls_field-name = 'numberOfDeliveryNotes'.
ls_field-type = 'decimal'.
ls_field-value = '1'.
APPEND ls_field TO ls_item-extended_data-fields.

CREATE OBJECT lo_subrecord.
lo_subrecord->name = 'volume'.
ls_field-name = 'unit'.
ls_field-type = 'string'.
ls_field-value = 'ccm'.
APPEND ls_field TO lo_subrecord->record-fields.

ls_field-name = 'value'.
ls_field-type = 'decimal'.
ls_field-value = '4500.000'.
APPEND ls_field TO lo_subrecord->record-fields.
APPEND lo_subrecord TO ls_item-extended_data-subrecords.

CREATE OBJECT lo_subrecord.
lo_subrecord->name = 'grossWeight'.
ls_field-name = 'unit'.
ls_field-type = 'string'.
ls_field-value = 'kg'.
APPEND ls_field TO lo_subrecord->record-fields.

ls_field-name = 'value'.
ls_field-type = 'decimal'.
ls_field-value = '1.900'.
APPEND ls_field TO lo_subrecord->record-fields.
APPEND lo_subrecord TO ls_item-extended_data-subrecords.

CREATE OBJECT lo_subrecord.
lo_subrecord->name = 'transportStart'.
CREATE OBJECT lo_subsubrecord.
lo_subsubrecord->name = 'postalAddress'.
ls_field-name = 'countryIsoCode'.
ls_field-type = 'string'.
ls_field-value = 'DE'.
APPEND ls_field TO lo_subsubrecord->record-fields.
ls_field-name = 'postcode'.
ls_field-type = 'string'.
ls_field-value = '70597'.
APPEND ls_field TO lo_subsubrecord->record-fields.
APPEND lo_subsubrecord TO lo_subrecord->record-subrecords.
APPEND lo_subrecord TO ls_item-extended_data-subrecords.

CREATE OBJECT lo_subrecord.
lo_subrecord->name = 'transportEnd'.
CREATE OBJECT lo_subsubrecord.
lo_subsubrecord->name = 'postalAddress'.
ls_field-name = 'countryIsoCode'.
ls_field-type = 'string'.
ls_field-value = 'DE'.
APPEND ls_field TO lo_subsubrecord->record-fields.
ls_field-name = 'postcode'.
ls_field-type = 'string'.
ls_field-value = '94405'.
APPEND ls_field TO lo_subsubrecord->record-fields.
APPEND lo_subsubrecord TO lo_subrecord->record-subrecords.
APPEND lo_subrecord TO ls_item-extended_data-subrecords.

CREATE OBJECT lo_subrecord.
lo_subrecord->name = 'packages'.
ls_field-name = 'dangerousGoodsHandlingCode'.
ls_field-type = 'string'.
ls_field-value = 'NONE'.
APPEND ls_field TO lo_subrecord->record-fields.
ls_field-name = 'packageReferenceNumber'.
ls_field-type = 'string'.
ls_field-value = 'package1'.
APPEND ls_field TO lo_subrecord->record-fields.
ls_field-name = 'numberOfPackages'.
ls_field-type = 'decimal'.
ls_field-value = '1'.
APPEND ls_field TO lo_subrecord->record-fields.
CREATE OBJECT lo_subsubrecord.
lo_subsubrecord->name = 'volume'.
ls_field-name = 'unit'.
ls_field-type = 'string'.
ls_field-value = 'ccm'.
APPEND ls_field TO lo_subsubrecord->record-fields.
ls_field-name = 'value'.
ls_field-type = 'decimal'.
ls_field-value = '1500.000'.
APPEND ls_field TO lo_subsubrecord->record-fields.
APPEND lo_subsubrecord to lo_subrecord->record-subrecords.
CREATE OBJECT lo_subsubrecord.
lo_subsubrecord->name = 'grossWeight'.
ls_field-name = 'unit'.
ls_field-type = 'string'.
ls_field-value = 'kg'.
APPEND ls_field TO lo_subsubrecord->record-fields.
ls_field-name = 'value'.
ls_field-type = 'decimal'.
ls_field-value = '0.600'.
APPEND ls_field TO lo_subsubrecord->record-fields.
APPEND lo_subsubrecord to lo_subrecord->record-subrecords.
CREATE OBJECT lo_subsubrecord.
lo_subsubrecord->name = 'dimensions'.
ls_field-name = 'length'.
ls_field-type = 'decimal'.
ls_field-value = '30.000'.
APPEND ls_field TO lo_subsubrecord->record-fields.
ls_field-name = 'width'.
ls_field-type = 'decimal'.
ls_field-value = '10.000'.
APPEND ls_field TO lo_subsubrecord->record-fields.
ls_field-name = 'quantityUnit'.
ls_field-type = 'string'.
ls_field-value = 'cm'.
APPEND ls_field TO lo_subsubrecord->record-fields.
ls_field-name = 'height'.
ls_field-type = 'decimal'.
ls_field-value = '5.000'.
APPEND ls_field TO lo_subsubrecord->record-fields.
APPEND lo_subsubrecord to lo_subrecord->record-subrecords.
APPEND lo_subrecord TO ls_item-extended_data-subrecords.

CREATE OBJECT lo_subrecord.
lo_subrecord->name = 'packages'.
ls_field-name = 'dangerousGoodsHandlingCode'.
ls_field-type = 'string'.
ls_field-value = 'NONE'.
APPEND ls_field TO lo_subrecord->record-fields.
ls_field-name = 'packageReferenceNumber'.
ls_field-type = 'string'.
ls_field-value = 'package2'.
APPEND ls_field TO lo_subrecord->record-fields.
ls_field-name = 'numberOfPackages'.
ls_field-type = 'decimal'.
ls_field-value = '1'.
APPEND ls_field TO lo_subrecord->record-fields.
CREATE OBJECT lo_subsubrecord.
lo_subsubrecord->name = 'volume'.
ls_field-name = 'unit'.
ls_field-type = 'string'.
ls_field-value = 'ccm'.
APPEND ls_field TO lo_subsubrecord->record-fields.
ls_field-name = 'value'.
ls_field-type = 'decimal'.
ls_field-value = '3000.000'.
APPEND ls_field TO lo_subsubrecord->record-fields.
APPEND lo_subsubrecord to lo_subrecord->record-subrecords.
CREATE OBJECT lo_subsubrecord.
lo_subsubrecord->name = 'grossWeight'.
ls_field-name = 'unit'.
ls_field-type = 'string'.
ls_field-value = 'kg'.
APPEND ls_field TO lo_subsubrecord->record-fields.
ls_field-name = 'value'.
ls_field-type = 'decimal'.
ls_field-value = '1.300'.
APPEND ls_field TO lo_subsubrecord->record-fields.
APPEND lo_subsubrecord to lo_subrecord->record-subrecords.
CREATE OBJECT lo_subsubrecord.
lo_subsubrecord->name = 'dimensions'.
ls_field-name = 'length'.
ls_field-type = 'decimal'.
ls_field-value = '30.000'.
APPEND ls_field TO lo_subsubrecord->record-fields.
ls_field-name = 'width'.
ls_field-type = 'decimal'.
ls_field-value = '20.000'.
APPEND ls_field TO lo_subsubrecord->record-fields.
ls_field-name = 'quantityUnit'.
ls_field-type = 'string'.
ls_field-value = 'cm'.
APPEND ls_field TO lo_subsubrecord->record-fields.
ls_field-name = 'height'.
ls_field-type = 'decimal'.
ls_field-value = '5.000'.
APPEND ls_field TO lo_subsubrecord->record-fields.
APPEND lo_subsubrecord to lo_subrecord->record-subrecords.
APPEND lo_subrecord TO ls_item-extended_data-subrecords.

APPEND ls_item TO lo_request->items.

lo_zlcm_rest_call->create_call(
  EXPORTING
    im_request = lo_request
    im_method  = 'createServiceItems'                 " N.n.
).
```

Of course you must adjust the fixed values to your needs. 

The method to use as exporting paramater is 'createServiceItems'. Please also see: [https://transport-freight-management.docs.developers.aeb.com/docs/the-first-service-item-1](https://transport-freight-management.docs.developers.aeb.com/docs/the-first-service-item-1)
