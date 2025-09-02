---
title: The first service item
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: Need extended Data? Then go on with handle extended data.
---
Use the API createServiceItem to create you first service item. 

```text ABAP
DATA:
  billing_bf             TYPE REF TO zco_ibilling_bf,
  output_data            TYPE zcreate_service_items_respons1,
  input_data             TYPE zcreate_service_items1,
  system_fault_exception TYPE REF TO cx_ai_system_fault,
  curr_message           LIKE LINE OF output_data-parameters-result-base-messages,
  curr_message_text      LIKE LINE OF curr_message-message_texts,
  item                   LIKE LINE OF input_data-parameters-request-items,
  item_result            TYPE zbservice_item_result_dto,
  field                  LIKE LINE OF item-extended_data-fields,
  subrecord              TYPE znamed_generic_data_record_dto,
  record                 LIKE item-extended_data.
TRY.
    CREATE OBJECT billing_bf EXPORTING logical_port_name = 'ZBILLING_BF_TEST2'.
  CATCH cx_ai_system_fault INTO system_fault_exception.
    WRITE 'Could not instantiate the billingBF '.
    WRITE system_fault_exception->get_text( ).
    RETURN.
ENDTRY.


input_data-parameters-request-base-client_ident_code = 'APITEST'.
input_data-parameters-request-base-client_system_id = 'T23_400'.
input_data-parameters-request-base-user_name = sy-uname.
APPEND 'EN' TO input_data-parameters-request-base-result_language_iso_codes.

input_data-parameters-request-parms-create_settlements_immediately = ' '.
input_data-parameters-request-parms-return_trace_info = 'X'.

item-beneficiary-base-name = 'AEB'.
item-beneficiary-base-city = 'Stuttgart'.
item-beneficiary-base-country_isocode = 'DE'.
item-beneficiary-base-company_number  = 'TNT_BE'.

item-charge_date-base-timezone = 'GMT+01:00'.
item-charge_date-base-date_in_timezone = '2019-05-20 13:11:35'.
item-client_orga_id = 'AEB_NORTH'.
item-client_system_cost_center = '1000'.
item-client_system_user-base-name = sy-uname.
item-description = 'API Test service item'.
item-item_id = 'API_TEST_ITEM_ID_01'.
item-order_date-base-timezone = 'GMT+01:00'.
item-order_date-base-date_in_timezone = '2019-05-20 13:11:35'.

item-orderer-base-name = 'AEB'.
item-orderer-base-city = 'Stuttgart'.
item-orderer-base-company_number  = 'TNT_BE'.
item-orderer-base-country_isocode = 'DE'.
item-orderer-base-street = 'Sigmaringerstraße 109'.
item-orderer-base-postcode = '70567'.

item-order_number = '4711'.

item-payer-base-name = 'AEB'.
item-payer-base-city = 'Stuttgart'.
item-payer-base-country_isocode = 'DE'.
item-payer-base-company_number  = 'TNT_BE'.
item-payer-base-street = 'Sigmaringerstraße 109'.
item-payer-base-postcode = '70567'.

item-quantity-base-unit = 'St'.
item-quantity-base-value = '1'.

item-reference_date-base-timezone = 'GMT+01:00'.
item-reference_date-base-date_in_timezone = '2019-05-20 13:11:35'.
item-reference_number = '4711'.

item-scenario_ident_code = '001'.
item-service_ident_code =  'TNTBE_EX09'.
item-service_provider-base-name = 'AEB'.
item-service_provider-base-city = 'Stuttgart'.
item-service_provider-base-company_number  = 'TNT_BE'.
item-service_provider-base-country_isocode = 'DE'.
item-service_provider-base-street = 'Sigmaringerstraße 109'.
item-service_provider-base-postcode = '70567'.

item-precalculated_net_price-base-currency_iso = 'EUR'.
item-precalculated_net_price-base-value = '100'.
item-pricing_date-base-timezone = 'GMT+01:00'.
item-pricing_date-base-date_in_timezone = '2019-05-20 13:11:35'.

APPEND item TO input_data-parameters-request-items.

TRY.
    billing_bf->create_service_items( EXPORTING input = input_data
                                      IMPORTING output = output_data ).

    LOOP AT output_data-parameters-result-base-messages INTO curr_message.
      READ TABLE curr_message-message_texts INTO curr_message_text INDEX 1.
      WRITE curr_message_text-text.
      WRITE /.
    ENDLOOP.

    LOOP AT output_data-parameters-result-base-messages INTO curr_message.
      READ TABLE curr_message-message_texts INTO curr_message_text INDEX 1.
      WRITE curr_message_text-text.
      WRITE /.
    ENDLOOP.

    LOOP AT output_data-parameters-result-item_results INTO item_result.
      IF item_result-base-has_errors <> 'X'.
        WRITE: item_result-item_id , ' is in status ' , item_result-status_ident_code, /.
      ENDIF.
      LOOP AT item_result-base-messages INTO curr_message.
        READ TABLE curr_message-message_texts INTO curr_message_text INDEX 1.
        WRITE curr_message_text-text.
        WRITE /.
      ENDLOOP.

    ENDLOOP.
  CATCH cx_ai_system_fault INTO system_fault_exception.
    WRITE 'Error when calling create service item '.
    WRITE system_fault_exception->get_text( ).
ENDTRY.
```
