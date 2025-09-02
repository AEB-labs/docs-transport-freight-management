---
title: Creation of the first document
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
The document consists out of two parts. The template and the document data. The template is stored in the Document service and will only be referenced in our ABAP program. The document data has to be transferred as JSON converted from an ABAP structure.  
We will maintain our template name as constant in the code. This example uses the template “DeliveryNote10.pdf”.  
To create the JSON content you have to know the data structure of the template. You can either get it from the XSD file or directly in the Document Service.

![](https://files.readme.io/15a102d-fd8d189-Bild1.png "fd8d189-Bild1.png")

This example code only contains part of the document structure. Variables like the destination names are hard coded and need to be adjusted according to your use case.

```text
*&---------------------------------------------------------------------*
*& Report ZSME_DOC_SERVICE_TEST
*&---------------------------------------------------------------------*
*&
*&---------------------------------------------------------------------*
REPORT zsme_doc_service_test.

TYPES:
  BEGIN OF companyaddress6l,
    addressline1 TYPE string,
    addressline2 TYPE string,
    addressline3 TYPE string,
    addressline4 TYPE string,
    addressline5 TYPE string,
    addressline6 TYPE string,
  END OF companyaddress6l .
TYPES:
  BEGIN OF shipmenttype,
    shipmenttype TYPE string,
  END OF shipmenttype .
TYPES:
  BEGIN OF referencedata,
    referenceascode128 TYPE string,
    referenceno        TYPE string,
    date               TYPE string,
    orderno            TYPE string,
    ordernocustomer    TYPE string,
    referenceno2       TYPE string,
    addreferenceinfo   TYPE string,
    contactperson      TYPE string,
    department         TYPE string,
    phone              TYPE string,
    email              TYPE string,
  END OF referencedata .
TYPES:
  BEGIN OF document_data,
    referencedata TYPE referencedata,
    consignor     TYPE companyaddress6l,
    buyer         TYPE companyaddress6l,
    consignee     TYPE companyaddress6l,
    notify        TYPE companyaddress6l,
    shipmenttype  TYPE shipmenttype,
  END OF document_data .

DATA: lt_json_contents TYPE TABLE OF document_data,
      ls_json_contents TYPE document_data
      .

ls_json_contents-consignee-addressline1 = 'AddressLine1'.
ls_json_contents-referencedata-referenceno = '12345'.
ls_json_contents-shipmenttype-shipmenttype = 'TEST'.


DATA: lv_body            TYPE string,
      lv_url             TYPE string,
      lv_async           TYPE string VALUE 'async=false',
      lv_processor       TYPE string VALUE 'processor=PDF-XFA',
*          lv_reference_type  TYPE string VALUE 'referenceType=SHIPMENT',
      lv_retention_limit TYPE string VALUE 'retentionDaysLimit=3',
      lv_format          TYPE string VALUE 'format=PDF',
      lv_document_name   TYPE string VALUE 'documentName=',
      lv_template        TYPE string VALUE 'templateName=',
      lv_reference       TYPE string VALUE 'referenceNumber=',
      lo_http_client     TYPE REF TO if_http_client,
      lo_rest_client     TYPE REF TO /iwcor/cl_rest_http_client,
      token              TYPE string,
      agreements         TYPE string,
      lo_response        TYPE REF TO /iwcor/if_rest_entity,
      lo_request         TYPE REF TO /iwcor/if_rest_entity,
      lv_http_status     TYPE string,
      lv_destination     TYPE CHAR20 VALUE 'ZSME_DOC_REST'
      .

/ui2/cl_json=>serialize(
  EXPORTING
    data             = ls_json_contents                 " Data to serialize
    compress         = 'X'                  " Skip empty elements
  RECEIVING
    r_json           = lv_body                 " JSON string
).

lv_document_name = lv_document_name && 'doc_name'.
lv_template = lv_template && 'DeliveryNote10.pdf'.
lv_reference = lv_reference && 'im_reference'.

CONCATENATE
lv_async
lv_processor
lv_template
lv_reference
*    lv_reference_type
lv_retention_limit
lv_format
lv_document_name
INTO
lv_url
SEPARATED BY '&'.

lv_url = '?' && lv_url.

cl_http_client=>create_by_destination(
 EXPORTING
   destination              = lv_destination    " Logical destination (specified in function call)
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
    WRITE: 'SUCCESS'.
    ELSE.
      WRITE: lv_http_status.
  ENDIF.

ENDIF.
```

Process result  
The result of the web service call is the PDF document in a binary stream. This stream can be converted back into PDF and for example stored on the local system. This will only work if processed in a user context as it uses the GUI_DOWNLOAD function. The binary can be obtained in above described example using lo_response->get_binary_data( ).

```text
*&---------------------------------------------------------------------*
*&      Form  process_result
*&---------------------------------------------------------------------*
*----------------------------------------------------------------------*

FORM process_result USING p_output TYPE zcreate_document_response1.
  DATA: lv_len     TYPE i,
        lt_content TYPE STANDARD TABLE OF tdline,
        lv_p_file  TYPE string,
        e_txt      TYPE REF TO cx_root.

  TRY.
      "Convert XSTRING to binary
      CALL FUNCTION 'SCMS_XSTRING_TO_BINARY'
        EXPORTING
          buffer        = p_output-parameters-result-document_content
        IMPORTING
          output_length = lv_len
        TABLES
          binary_tab    = lt_content.

      "Export binary (PDF) to file system
      CONCATENATE
      'C:\tmp\result\result'
      sy-datum
      sy-timlo
      INTO lv_p_file
      SEPARATED BY '_'.
      lv_p_file = lv_p_file && '.pdf'.
      CALL FUNCTION 'GUI_DOWNLOAD'
        EXPORTING
          filename                = lv_p_file
          filetype                = 'BIN'
        TABLES
          data_tab                = lt_content
*         FIELDNAMES              =
        EXCEPTIONS
          file_write_error        = 1
          no_batch                = 2
          gui_refuse_filetransfer = 3
          invalid_type            = 4
          no_authority            = 5
          unknown_error           = 6
          header_not_allowed      = 7
          separator_not_allowed   = 8
          filesize_not_allowed    = 9
          header_too_long         = 10
          dp_error_create         = 11
          dp_error_send           = 12
          dp_error_write          = 13
          unknown_dp_error        = 14
          access_denied           = 15
          dp_out_of_memory        = 16
          disk_full               = 17
          dp_timeout              = 18
          file_not_found          = 19
          dataprovider_exception  = 20
          control_flush_error     = 21
          OTHERS                  = 22.

    CATCH cx_root INTO e_txt.

  ENDTRY.
ENDFORM.
```

The form will just be provided with the output data like this:

```text
PERFORM process_result USING output_data.
```