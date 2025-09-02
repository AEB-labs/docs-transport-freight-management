---
title: Get result of a routing task
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
Now that you have created a routing task the next step is to get the result of that routing task. The calculation of a routing task runs asynchronously. So you have to call another API to get the result of the calculation.
[block:code]
{
  "codes": [
    {
      "code": "PARAMETERS: p_tsk_id type c LENGTH 40.\n\nDATA:\n  routing_bf             TYPE REF TO zco_irouting_bf,\n  output_data            TYPE zget_routing_task_result_resp2,\n  input_data             TYPE zget_routing_task_result1,\n  system_fault_exception TYPE REF TO cx_ai_system_fault,\n  curr_message           LIKE LINE OF output_data-parameters-result-base-messages,\n  curr_message_text      LIKE LINE OF curr_message-message_texts.\n\nTRY.\n    CREATE OBJECT routing_bf EXPORTING logical_port_name = 'ZROUTING_BF_TEST1'.\n  CATCH cx_ai_system_fault INTO system_fault_exception.\n    WRITE 'Could not instantiate the routingBF '.\n    WRITE /.\n    WRITE system_fault_exception->get_text( ).\n    WRITE /.\n    RETURN.\nENDTRY.\n\n\ninput_data-parameters-request-base-client_ident_code = 'APITEST'.\ninput_data-parameters-request-base-client_system_id = 'T23_400'.\ninput_data-parameters-request-base-user_name = sy-uname.\nAPPEND 'EN' TO input_data-parameters-request-base-result_language_iso_codes.\n\ninput_data-parameters-request-task_id = p_tsk_id.\n\nTRY.\n    routing_bf->get_routing_task_result( EXPORTING input = input_data\n                                         IMPORTING output = output_data ).\n\n    LOOP AT output_data-parameters-result-base-messages INTO curr_message.\n      READ TABLE curr_message-message_texts INTO curr_message_text INDEX 1.\n      WRITE curr_message_text-text.\n      WRITE /.\n    ENDLOOP.\n\n    IF output_data-parameters-result-base-has_errors = 'X'.\n      WRITE 'Could not get the referenced routing task with id'.\n      write input_data-parameters-request-task_id.\n    ELSE.\n      WRITE 'Could get the routing task with id '.\n      write input_data-parameters-request-task_id.\n      write /.\n      write 'The state of the routing task ist '.\n      WRITE output_data-parameters-result-routing_task_result-state.\n    ENDIF.\n\n\n  CATCH cx_ai_system_fault INTO system_fault_exception.\n    WRITE 'Error when calling get routing task result'.\n    WRITE /.\n    WRITE system_fault_exception->get_text( ).\nENDTRY.",
      "language": "text",
      "name": "ABAP"
    }
  ]
}
[/block]
If there were no errors in the result you have the state of the routing task in the result. There are three possible values:
- INPROGRESS: proposals (and ordering) might change in future calls.
- RANKED: ordering and proposals fixed, at least one supplement missing.
- COMPLETE: ordering and entries fixed, all supplements calculated.