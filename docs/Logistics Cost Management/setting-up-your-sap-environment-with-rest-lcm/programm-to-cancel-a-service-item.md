---
title: Program to cancel a service item
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Please treat this program as example. You can integrate the call in your SAP system where it suits your process most.

In order to use this you need to store the item id in an appropriate place in SAP or must be able to re-produce it.

```Text Cancel service item
*&---------------------------------------------------------------------*
*& Report ZSME_CANCEL_LCM_SERVICE_ITEM
*&---------------------------------------------------------------------*
*&
*&---------------------------------------------------------------------*
REPORT zlcm_cancel_lcm_service_item.

DATA: lo_request TYPE REF TO zlcm_cancel_item_request,
      ls_item    TYPE zlcm_cancel_item_request=>item
      .

CREATE OBJECT lo_request.

DATA(lo_zlcm_lcm_rest_call) = zlcm_rest_call=>new_for( im_destination = 'NAME' ).

lo_request->client_ident_code = 'CLIENT'.
lo_request->client_system_id = sy-sysid && '_' && sy-mandt.
lo_request->reason_of_reversal = 'TEST'.
APPEND 'de' TO lo_request->resultlanguage_iso_codes.
lo_request->user_name = sy-uname.

ls_item-item_id = '25-11-2022'.
APPEND ls_item TO lo_request->items.

lo_zlcm_lcm_rest_call->create_call(
  EXPORTING
    im_request = lo_request
    im_method  = 'cancelServiceItems'                 " N.n.
).
```

The method to use as exporting parameter is named 'cancelServiceItems'.