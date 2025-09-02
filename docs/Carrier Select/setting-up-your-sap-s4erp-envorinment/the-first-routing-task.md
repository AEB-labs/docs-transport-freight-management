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
[block:code]
{
  "codes": [
    {
      "code": "DATA:\n  routing_bf             TYPE REF TO zco_irouting_bf,\n  output_data            TYPE zcreate_routing_task_response1,\n  input_data             TYPE zcreate_routing_task1,\n  system_fault_exception TYPE REF TO cx_ai_system_fault,\n  curr_message           LIKE LINE OF output_data-parameters-result-base-messages,\n  curr_message_text      LIKE LINE OF curr_message-message_texts,\n  handling_unit          LIKE LINE OF input_data-parameters-request-routing_task-handling_units.\n\nTRY.\n    CREATE OBJECT routing_bf EXPORTING logical_port_name = 'ZROUTING_BF_TEST1'.\n  CATCH cx_ai_system_fault INTO system_fault_exception.\n    WRITE 'Could not instantiate the routingBF '.\n    WRITE /.\n    WRITE system_fault_exception->get_text( ).\n    WRITE /.\n    RETURN.\nENDTRY.\n\n\ninput_data-parameters-request-base-client_ident_code = 'APITEST'.\ninput_data-parameters-request-base-client_system_id = 'T23_400'.\ninput_data-parameters-request-base-user_name = sy-uname.\nAPPEND 'EN' to input_data-parameters-request-base-result_language_iso_codes.\n\ninput_data-parameters-request-routing_task-decisive_date = '2019-05-16'.\ninput_data-parameters-request-routing_task-reference_number = 'API_TEST_01'.\n\nhandling_unit-handling_unit_type = 'DUMMY'.\nhandling_unit-number_of_handling_units = 5.\nhandling_unit-single_dimensions-height = '100'.\nhandling_unit-single_dimensions-length = '100'.\nhandling_unit-single_dimensions-width = '100'.\nhandling_unit-single_dimensions-quantity_unit = 'cm'.\nhandling_unit-single_gross_weight-unit = 'kg'.\nhandling_unit-single_gross_weight-value = '1'.\nAPPEND handling_unit TO input_data-parameters-request-routing_task-handling_units.\n\ninput_data-parameters-request-routing_task-start_location-address-country_isocode = 'DE'.\ninput_data-parameters-request-routing_task-start_location-address-city = 'Stuttgart'.\ninput_data-parameters-request-routing_task-start_location-address-postcode = '70772'.\ninput_data-parameters-request-routing_task-start_location-address-street = 'Grünweg 3'.\ninput_data-parameters-request-routing_task-start_location-address-name = 'Anja Müller'.\n\ninput_data-parameters-request-routing_task-end_location-address-country_isocode = 'DE'.\ninput_data-parameters-request-routing_task-end_location-address-city = 'Leinfelden'.\ninput_data-parameters-request-routing_task-end_location-address-postcode = '70771'.\ninput_data-parameters-request-routing_task-end_location-address-street = 'Gustlestraße 5'.\ninput_data-parameters-request-routing_task-end_location-address-name = 'Thomas Meier'.\n\nTRY.\n    routing_bf->create_routing_task( EXPORTING input = input_data\n                                     IMPORTING output = output_data ).\n\n    LOOP AT output_data-parameters-result-base-messages INTO curr_message.\n      READ TABLE curr_message-message_texts INTO curr_message_text INDEX 1.\n      WRITE curr_message_text-text.\n      WRITE /.\n    ENDLOOP.\n\n    if output_data-parameters-result-base-has_errors = 'X'.\n      write 'Could not create a routing task.'.\n    else.\n      write 'Could create a routing task with id '.\n      write output_data-parameters-result-task_id.\n    endif.\n\n\n  CATCH cx_ai_system_fault INTO system_fault_exception.\n    WRITE 'Error when calling create routing task '.\n    WRITE /.\n    WRITE system_fault_exception->get_text( ).\nENDTRY.",
      "language": "text",
      "name": "ABAP"
    }
  ]
}
[/block]
If there were no errors the ID of the routing task will be part of the result. The next step is to get the result of routing task. For that you have to remember the ID of your routing task.