---
title: Setting up the REST call class
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
      slug: programm-to-create-a-service-item
      title: Program to create a service item
---
This class will provide you the possibility to use all methods of the billing API.  
Use the static NEW_FOR method as constructor. It imports the name of the SM59 connection you created.

```
class ZLCM_REST_CALL definition
  public
  final
  create public .

public section.

  methods CREATE_CALL
    importing
      !IM_REQUEST type DATA
      !IM_METHOD type /AEB/01_CHAR100 .
  class-methods NEW_FOR
    importing
      !IM_DESTINATION type C
    returning
      value(RE_VALUE) type ref to ZLCM_REST_CALL .
protected section.
private section.

  data GV_REST_DEST type /AEB/01_CHAR20 .
ENDCLASS.



CLASS ZLCM_REST_CALL IMPLEMENTATION.


* <SIGNATURE>---------------------------------------------------------------------------------------+
* | Instance Public Method ZLCM_REST_CALL->CREATE_CALL
* +-------------------------------------------------------------------------------------------------+
* | [--->] IM_REQUEST                     TYPE        DATA
* | [--->] IM_METHOD                      TYPE        /AEB/01_CHAR100
* +--------------------------------------------------------------------------------------</SIGNATURE>
  METHOD CREATE_CALL.

    DATA: lv_body        TYPE string,
          lv_url         TYPE string,
          lo_rest_client TYPE REF TO /iwcor/cl_rest_http_client,
          token          TYPE string,
          agreements     TYPE string,
          lo_http_client TYPE REF TO if_http_client,
          lo_response    TYPE REF TO /iwcor/if_rest_entity,
          lo_request     TYPE REF TO /iwcor/if_rest_entity,
          lv_http_status TYPE string
          .

    /ui2/cl_json=>serialize(
      EXPORTING
        data             = im_request                 " Data to serialize
        compress         = 'X'                  " Skip empty elements
        pretty_name     = 'X'
      RECEIVING
        r_json           = lv_body                 " JSON string
    ).

    IF im_method(1) <> '/'.
      lv_url = '/' && im_method.
    ELSE.
      lv_url = im_method.
    ENDIF.

    cl_http_client=>create_by_destination(
     EXPORTING
       destination              = gv_rest_dest    " Logical destination (specified in function call)
     IMPORTING
       client                   = lo_http_client    " HTTP Client Abstraction
     EXCEPTIONS
       argument_not_found       = 1
       destination_not_found    = 2
       destination_no_authority = 3
       plugin_not_active        = 4
       internal_error           = 5
       OTHERS                   = 6
    ).

    CREATE OBJECT lo_rest_client
      EXPORTING
        io_http_client = lo_http_client.

    lo_http_client->request->set_version( if_http_request=>co_protocol_version_1_0 ).
    IF lo_http_client IS BOUND AND lo_rest_client IS BOUND.

      cl_http_utility=>set_request_uri(
        EXPORTING
          request = lo_http_client->request    " HTTP Framework (iHTTP) HTTP Request
          uri     = lv_url                     " URI String (in the Form of /path?query-string)
      ).

      CALL METHOD lo_rest_client->/iwcor/if_rest_client~set_request_header
        EXPORTING
          iv_name  = 'auth-token'
          iv_value = token.

      lo_request = lo_rest_client->/iwcor/if_rest_client~create_request_entity( ).
      lo_request->set_content_type( EXPORTING iv_media_type = /iwcor/if_rest_media_type=>gc_appl_json ).

      SHIFT lv_body LEFT DELETING LEADING '['.
      SHIFT lv_body RIGHT DELETING TRAILING ']'.

      lo_request->set_string_data( lv_body ).
      lo_rest_client->/iwcor/if_rest_resource~post( io_entity = lo_request ).

      lo_response = lo_rest_client->/iwcor/if_rest_client~get_response_entity( ).

      lv_http_status = lo_response->get_header_field( '~status_code' ).

      IF lv_http_status <> '200'.
        RETURN.
      ENDIF.

    ENDIF.

  ENDMETHOD.


* <SIGNATURE>---------------------------------------------------------------------------------------+
* | Static Public Method ZLCM_REST_CALL=>NEW_FOR
* +-------------------------------------------------------------------------------------------------+
* | [--->] IM_DESTINATION                 TYPE        C
* | [<-()] RE_VALUE                       TYPE REF TO ZLCM_REST_CALL
* +--------------------------------------------------------------------------------------</SIGNATURE>
  METHOD NEW_FOR.

    CREATE OBJECT re_value.

    re_value->gv_rest_dest = im_destination.

  ENDMETHOD.
ENDCLASS.
```

The CREATE_CALL method is used to create the actual API call. It requires the name of the method to call and a structure or object that will then be converted into JSON.

Feel free to adjust or propose changes!