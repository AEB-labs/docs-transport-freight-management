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

```text ABAP
PARAMETERS: p_tsk_id type c LENGTH 40.

DATA:
  routing_bf             TYPE REF TO zco_irouting_bf,
  output_data            TYPE zget_routing_task_result_resp2,
  input_data             TYPE zget_routing_task_result1,
  system_fault_exception TYPE REF TO cx_ai_system_fault,
  curr_message           LIKE LINE OF output_data-parameters-result-base-messages,
  curr_message_text      LIKE LINE OF curr_message-message_texts.

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
APPEND 'EN' TO input_data-parameters-request-base-result_language_iso_codes.

input_data-parameters-request-task_id = p_tsk_id.

TRY.
    routing_bf->get_routing_task_result( EXPORTING input = input_data
                                         IMPORTING output = output_data ).

    LOOP AT output_data-parameters-result-base-messages INTO curr_message.
      READ TABLE curr_message-message_texts INTO curr_message_text INDEX 1.
      WRITE curr_message_text-text.
      WRITE /.
    ENDLOOP.

    IF output_data-parameters-result-base-has_errors = 'X'.
      WRITE 'Could not get the referenced routing task with id'.
      write input_data-parameters-request-task_id.
    ELSE.
      WRITE 'Could get the routing task with id '.
      write input_data-parameters-request-task_id.
      write /.
      write 'The state of the routing task ist '.
      WRITE output_data-parameters-result-routing_task_result-state.
    ENDIF.


  CATCH cx_ai_system_fault INTO system_fault_exception.
    WRITE 'Error when calling get routing task result'.
    WRITE /.
    WRITE system_fault_exception->get_text( ).
ENDTRY.
```

If there were no errors in the result you have the state of the routing task in the result. There are three possible values:

* INPROGRESS: proposals (and ordering) might change in future calls.
* RANKED: ordering and proposals fixed, at least one supplement missing.
* COMPLETE: ordering and entries fixed, all supplements calculated.
