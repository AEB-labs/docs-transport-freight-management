---
title: The first routing task
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: >-
    Created your first routing task. Ok then go on with getting the result of
    the routing task.
  pages:
    - type: basic
      slug: get-result-of-a-routing-task
      title: Get result of a routing task
---
Your target is to select a carrier. For that you have to put a routing task to Carrier Select. For that you need some basic data. Just use the following Code-Snippet to create your first routing task.

```text ABAP
DATA:
  routing_bf             TYPE REF TO zco_irouting_bf,
  output_data            TYPE zcreate_routing_task_response1,
  input_data             TYPE zcreate_routing_task1,
  system_fault_exception TYPE REF TO cx_ai_system_fault,
  curr_message           LIKE LINE OF output_data-parameters-result-base-messages,
  curr_message_text      LIKE LINE OF curr_message-message_texts,
  handling_unit          LIKE LINE OF input_data-parameters-request-routing_task-handling_units.

TRY.
    CREATE OBJECT routing_bf EXPORTING logical_port_name = 'ZROUTING_BF_TEST1'.
  CATCH cx_ai_system_fault INTO system_fault_exception.
    WRITE 'Could not instantiate the routingBF '.
    WRITE /.
    WRITE system_fault_exception->get_text( ).
    WRITE /.
    RETURN.
ENDTRY.


input_data-parameters-request-base-client_ident_code = 'APITEST'.
input_data-parameters-request-base-client_system_id = 'T23_400'.
input_data-parameters-request-base-user_name = sy-uname.
APPEND 'EN' to input_data-parameters-request-base-result_language_iso_codes.

input_data-parameters-request-routing_task-decisive_date = '2019-05-16'.
input_data-parameters-request-routing_task-reference_number = 'API_TEST_01'.

handling_unit-handling_unit_type = 'DUMMY'.
handling_unit-number_of_handling_units = 5.
handling_unit-single_dimensions-height = '100'.
handling_unit-single_dimensions-length = '100'.
handling_unit-single_dimensions-width = '100'.
handling_unit-single_dimensions-quantity_unit = 'cm'.
handling_unit-single_gross_weight-unit = 'kg'.
handling_unit-single_gross_weight-value = '1'.
APPEND handling_unit TO input_data-parameters-request-routing_task-handling_units.

input_data-parameters-request-routing_task-start_location-address-country_isocode = 'DE'.
input_data-parameters-request-routing_task-start_location-address-city = 'Stuttgart'.
input_data-parameters-request-routing_task-start_location-address-postcode = '70772'.
input_data-parameters-request-routing_task-start_location-address-street = 'Grünweg 3'.
input_data-parameters-request-routing_task-start_location-address-name = 'Anja Müller'.

input_data-parameters-request-routing_task-end_location-address-country_isocode = 'DE'.
input_data-parameters-request-routing_task-end_location-address-city = 'Leinfelden'.
input_data-parameters-request-routing_task-end_location-address-postcode = '70771'.
input_data-parameters-request-routing_task-end_location-address-street = 'Gustlestraße 5'.
input_data-parameters-request-routing_task-end_location-address-name = 'Thomas Meier'.

TRY.
    routing_bf->create_routing_task( EXPORTING input = input_data
                                     IMPORTING output = output_data ).

    LOOP AT output_data-parameters-result-base-messages INTO curr_message.
      READ TABLE curr_message-message_texts INTO curr_message_text INDEX 1.
      WRITE curr_message_text-text.
      WRITE /.
    ENDLOOP.

    if output_data-parameters-result-base-has_errors = 'X'.
      write 'Could not create a routing task.'.
    else.
      write 'Could create a routing task with id '.
      write output_data-parameters-result-task_id.
    endif.


  CATCH cx_ai_system_fault INTO system_fault_exception.
    WRITE 'Error when calling create routing task '.
    WRITE /.
    WRITE system_fault_exception->get_text( ).
ENDTRY.
```

If there were no errors the ID of the routing task will be part of the result. The next step is to get the result of routing task. For that you have to remember the ID of your routing task.
