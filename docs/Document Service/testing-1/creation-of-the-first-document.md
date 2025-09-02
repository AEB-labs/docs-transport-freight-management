---
title: Creation of the first document
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
The document consists out of two parts. The template and the document data. The template is stored in the Document service and will only be referenced in our ABAP program. The document data has to be transferred as XML converted into a binary XSTRING.\
We will maintain our template name as constant in the code. This example uses the template “DeliveryNote10.pdf”.\
To create the XML content you have to know the data structure of the template. You can either get it from the XSD file or directly in the Document Service.

![605](https://files.readme.io/fd8d189-Bild1.png "Bild1.png")

The XML elements are basically all key value pairs so the easiest way is to create a sub form to create the XML elements based on a table of key value pairs. We will define the table of key value pairs as our own data type and three different forms depending on the type of data we want to add to the XML:

* ADD\_FIELDS (will simply add fields to the root element)
* ADD\_ELEMENT (adds a sub element to the document which contains own fields)
* ADD\_NODE (adds a node which can have both fields and sub elements)\
  As this is an example the values for the fields are just the field names.

```text
TYPES: BEGIN OF key_value_pair,
         key   TYPE string,
         value TYPE string,
       END OF key_value_pair.

TYPES: t_key_value_pairs TYPE TABLE OF key_value_pair WITH DEFAULT KEY.

TYPES: BEGIN OF new_node,
         node_name          TYPE string,
         ref_ixml_node      TYPE REF TO if_ixml_node,
         tt_key_value_pairs TYPE t_key_value_pairs,
       END OF new_node.

TYPES: BEGIN OF new_field,
         tt_key_value_pairs TYPE t_key_value_pairs,
       END OF new_field.

DATA:
  document_service_bf    TYPE REF TO zco_idocument_service_bf,
  output_data            TYPE zcreate_document_response1,
  input_data             TYPE zcreate_document1,
  system_fault_exception TYPE REF TO cx_ai_system_fault,
  soap_fault_excepton    TYPE REF TO cx_ai_soap_fault,
  lv_content_string      TYPE xstring.

CONSTANTS: lcv_template_name TYPE string VALUE 'DeliveryNote10.pdf'.

"Instatiate BF
TRY.
    CREATE OBJECT document_service_bf EXPORTING logical_port_name = 'ZDOCUMENT_SERVICE_BF_TEST'.
  CATCH cx_ai_system_fault INTO system_fault_exception.
    WRITE 'Could not instantiate the document_bf'.
    WRITE system_fault_exception->get_text( ).
    RETURN.
ENDTRY.

PERFORM create_xml_data USING lv_content_string.

"BF parameters: template
input_data-parameters-request-template-processor = 'PDF-XFA'.
input_data-parameters-request-template-filename = lcv_template_name.
"BF parameters: job_processing_options
input_data-parameters-request-job_processing_options-is_trace = 'X'.
input_data-parameters-request-job_processing_options-timeout = 60000.
input_data-parameters-request-job_processing_options-timeout_submit = 10000.
input_data-parameters-request-job_processing_options-user_locale = 'DE'.
"BF parameters: document_processing_options
input_data-parameters-request-document_processing_options-format = 'PDF'.
input_data-parameters-request-document_processing_options-is_return_page_mapping = 'X'.
"BF parameters: xml_data
input_data-parameters-request-xml_data = lv_content_string.

"Execute BF call
TRY.
    document_service_bf->create_document( EXPORTING  input = input_data
                           IMPORTING output = output_data ).

  CATCH cx_ai_soap_fault INTO soap_fault_excepton.
    WRITE soap_fault_excepton->get_text( ).
  CATCH cx_ai_system_fault INTO system_fault_exception.
    WRITE system_fault_exception->get_text( ).
ENDTRY.


*&---------------------------------------------------------------------*
*&      Form  create_xml_data
*&---------------------------------------------------------------------*
*----------------------------------------------------------------------*
FORM create_xml_data USING p_lv_content_string TYPE xstring.
  TYPES : my_type TYPE c LENGTH 60.
  DATA: ref_ixml_node_parent    TYPE REF TO if_ixml_node,
        lt_t_key_value_pairs    TYPE t_key_value_pairs,
        ls_t_key_value_pairs    TYPE key_value_pair,
        ls_new_node             TYPE new_node,
        lv_node_name            TYPE string,
        ref_ixml                TYPE REF TO if_ixml,
        ref_ixml_document       TYPE REF TO if_ixml_document,
        lif_ixml_stream_factory TYPE REF TO if_ixml_stream_factory,
        ref_ixml_ostream        TYPE REF TO if_ixml_ostream,
        lt_string               TYPE TABLE OF my_type,
        ref_ixml_encoding       TYPE REF TO if_ixml_encoding,
        ref_ixml_renderer       TYPE REF TO if_ixml_renderer,
        ref_ixml_element        TYPE REF TO if_ixml_element.

  CONSTANTS: mc_character_set  TYPE string VALUE 'TEST*'.

  "Set XML parameters and create factory, stream and renderer
**-- Create the Main XML Factory
  ref_ixml = cl_ixml=>create( ).
**-- Create the Initial Document
  ref_ixml_document = ref_ixml->create_document( ).
**-- Create an Output Stream
  lif_ixml_stream_factory = ref_ixml->create_stream_factory( ).
  ref_ixml_ostream = lif_ixml_stream_factory->create_ostream_itable( table = lt_string ).

**-- Create an Encoding
  ref_ixml_encoding = ref_ixml->create_encoding(
    byte_order    = 0
    character_set = mc_character_set
  ).

**-- Set the Encoding
  ref_ixml_ostream->set_encoding( encoding = ref_ixml_encoding ).

**-- Create a Renderer
  ref_ixml_renderer = ref_ixml->create_renderer(
    document = ref_ixml_document
    ostream  = ref_ixml_ostream
  ).

  "Create content XML structure
  "Create basic structure
  "Root node is always documentData
**-- Create the Root Node
  ref_ixml_element = ref_ixml_document->create_element(
    name      = 'documentData'
  ).
**-- Append the Root element to the Document
  ref_ixml_document->append_child( new_child = ref_ixml_element ).

**-- Define a Parent Node
  "Define root node as parent
  ref_ixml_node_parent = ref_ixml_element.

  "======================================================================
  "DATA SECTION
  "======================================================================
  "Create next level according to PDFXFA structure
  CLEAR: lt_t_key_value_pairs.

  "Create fields on parent level
  ls_t_key_value_pairs-key = 'ConsigneeCustomerNo'.
  ls_t_key_value_pairs-value = 'ConsigneeCustomerNo'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'Consignee5Lines'.
  ls_t_key_value_pairs-value = 'Consignee5Lines'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'ContactPersonDepartment'.
  ls_t_key_value_pairs-value = 'ContactPersonDepartment'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'ContactPersonName'.
  ls_t_key_value_pairs-value = 'ContactPersonName'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'ContactPersonEMail'.
  ls_t_key_value_pairs-value = 'ContactPersonEMail'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'ContactPersonPhone'.
  ls_t_key_value_pairs-value = 'ContactPersonPhone'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'CurrentDate'.
  ls_t_key_value_pairs-value = 'CurrentDate'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'DeliveryNoteNo'.
  ls_t_key_value_pairs-value = 'DeliveryNoteNo'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'DispatchType'.
  ls_t_key_value_pairs-value = 'DispatchType'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'ForwarderName'.
  ls_t_key_value_pairs-value = 'ForwarderName'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'FooterLineLeft'.
  ls_t_key_value_pairs-value = 'FooterLineLeft'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'FooterLineMiddle1'.
  ls_t_key_value_pairs-value = 'FooterLineMiddle1'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'FooterLineMiddle2'.
  ls_t_key_value_pairs-value = 'FooterLineMiddle2'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'FooterLineRight'.
  ls_t_key_value_pairs-value = 'FooterLineRight'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'Incoterm'.
  ls_t_key_value_pairs-value = 'Incoterm'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'OrderDate'.
  ls_t_key_value_pairs-value = 'OrderDate'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'OrderDateCustomer'.
  ls_t_key_value_pairs-value = 'OrderDateCustomer'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'OrderNumber'.
  ls_t_key_value_pairs-value = 'OrderNumber'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'OrderNoCustomer'.
  ls_t_key_value_pairs-value = 'OrderNoCustomer'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'Remarks'.
  ls_t_key_value_pairs-value = 'Remarks'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'ShipperContact'.
  ls_t_key_value_pairs-value = 'ShipperContact'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'ShippingDate'.
  ls_t_key_value_pairs-value = 'ShippingDate'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'ShippingPoint5Lines'.
  ls_t_key_value_pairs-value = 'ShippingPoint5Lines'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'ShippingPointOneLineAddress'.
  ls_t_key_value_pairs-value = 'ShippingPointOneLineAddress'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  ls_t_key_value_pairs-key = 'ServiceType'.
  ls_t_key_value_pairs-value = 'ServiceType'.
  APPEND ls_t_key_value_pairs TO lt_t_key_value_pairs.

  PERFORM add_fields USING ref_ixml_document ref_ixml_node_parent lt_t_key_value_pairs.

  "Items
  CLEAR: ls_new_node.
  ls_new_node-node_name = 'DeliveryNoteItems'.

  ls_t_key_value_pairs-key = 'ItemDescription'.
  ls_t_key_value_pairs-value = 'ItemDescription'.
  APPEND ls_t_key_value_pairs TO ls_new_node-tt_key_value_pairs.

  ls_t_key_value_pairs-key = 'ItemNo'.
  ls_t_key_value_pairs-value = 'ItemNo'.
  APPEND ls_t_key_value_pairs TO ls_new_node-tt_key_value_pairs.

  ls_t_key_value_pairs-key = 'ItemNoCustomer'.
  ls_t_key_value_pairs-value = 'ItemNoCustomer'.
  APPEND ls_t_key_value_pairs TO ls_new_node-tt_key_value_pairs.

  ls_t_key_value_pairs-key = 'ItemQuantity'.
  ls_t_key_value_pairs-value = 'ItemQuantity'.
  APPEND ls_t_key_value_pairs TO ls_new_node-tt_key_value_pairs.

  ls_t_key_value_pairs-key = 'ItemRemark'.
  ls_t_key_value_pairs-value = 'ItemRemark'.
  APPEND ls_t_key_value_pairs TO ls_new_node-tt_key_value_pairs.

  ls_t_key_value_pairs-key = 'OrderNo'.
  ls_t_key_value_pairs-value = 'OrderNo'.
  APPEND ls_t_key_value_pairs TO ls_new_node-tt_key_value_pairs.

  ls_t_key_value_pairs-key = 'OrderNoCustomer'.
  ls_t_key_value_pairs-value = 'OrderNoCustomer'.
  APPEND ls_t_key_value_pairs TO ls_new_node-tt_key_value_pairs.

  ls_t_key_value_pairs-key = 'ProductNo'.
  ls_t_key_value_pairs-value = 'ProductNo'.
  APPEND ls_t_key_value_pairs TO ls_new_node-tt_key_value_pairs.

  PERFORM add_element USING ref_ixml_document ref_ixml_node_parent ls_new_node.

  "Buyer
  CLEAR: ls_new_node.
  ls_new_node-node_name = 'Buyer'.

  ls_t_key_value_pairs-key = 'Buyer5Lines'.
  ls_t_key_value_pairs-value = 'Buyer5Lines'.
  APPEND ls_t_key_value_pairs TO ls_new_node-tt_key_value_pairs.

  PERFORM add_element USING ref_ixml_document ref_ixml_node_parent ls_new_node.

  "Create XML XSTRING from XML DOM
  CALL FUNCTION 'SDIXML_DOM_TO_XML'
    EXPORTING
      document      = ref_ixml_document
    IMPORTING
      xml_as_string = p_lv_content_string
    EXCEPTIONS
      no_document   = 1
      OTHERS        = 2.
  IF sy-subrc <> 0.
**--Exception Handling

  ENDIF.
ENDFORM.

*&---------------------------------------------------------------------*
*&      Form  ADD_ELEMENT
*&---------------------------------------------------------------------*
*----------------------------------------------------------------------*
FORM add_element  USING  p_ref_ixml_document    TYPE REF TO if_ixml_document
                      p_ref_ixml_node_parent TYPE REF TO if_ixml_node
                      p_new_node TYPE new_node
                      .

  DATA lo_ref_ixml_element     TYPE REF TO if_ixml_element .
  DATA lo_ref_ixml_element_sub TYPE REF TO if_ixml_element .
  DATA lv_key_value_pair TYPE  key_value_pair.


  lo_ref_ixml_element = p_ref_ixml_document->create_element(
      name      = p_new_node-node_name
  ).

  p_ref_ixml_node_parent->append_child( new_child = lo_ref_ixml_element ).

  LOOP AT p_new_node-tt_key_value_pairs INTO lv_key_value_pair.
    lo_ref_ixml_element_sub = p_ref_ixml_document->create_element( name = lv_key_value_pair-key ).
    lo_ref_ixml_element_sub->set_value( value = lv_key_value_pair-value ).
    lo_ref_ixml_element->append_child( new_child = lo_ref_ixml_element_sub ).
  ENDLOOP.

ENDFORM.

*&---------------------------------------------------------------------*
*&      Form  ADD_FIELDS
*&---------------------------------------------------------------------*
*----------------------------------------------------------------------*
FORM add_fields  USING  p_ref_ixml_document    TYPE REF TO if_ixml_document
                      p_ref_ixml_node_parent TYPE REF TO if_ixml_node
                      p_new_fields TYPE t_key_value_pairs
                      .

  DATA lo_ref_ixml_element     TYPE REF TO if_ixml_element .
  DATA lo_ref_ixml_element_sub TYPE REF TO if_ixml_element .
  DATA lv_key_value_pair TYPE  key_value_pair.

  LOOP AT p_new_fields INTO lv_key_value_pair.
    lo_ref_ixml_element = p_ref_ixml_document->create_element( name      = lv_key_value_pair-key  ).
    lo_ref_ixml_element->set_value( value = lv_key_value_pair-value ).

    p_ref_ixml_node_parent->append_child( new_child = lo_ref_ixml_element ).
  ENDLOOP.
ENDFORM.

*&---------------------------------------------------------------------*
*&      Form  ADD_NODE
*&---------------------------------------------------------------------*
*----------------------------------------------------------------------*
FORM add_node  USING  p_ref_ixml_document    TYPE REF TO if_ixml_document
                      p_ref_ixml_node_parent TYPE REF TO if_ixml_node
                      p_new_node TYPE new_node
                      .

  DATA lo_ref_ixml_node     TYPE REF TO if_ixml_node .
  DATA lo_ref_ixml_element TYPE REF TO if_ixml_element .
  DATA lv_key_value_pair TYPE  key_value_pair.

  IF p_new_node-ref_ixml_node IS INITIAL.
    lo_ref_ixml_node = p_ref_ixml_document->create_element(
        name      = p_new_node-node_name
    ).
    p_new_node-ref_ixml_node = lo_ref_ixml_node.
  ELSE.
    lo_ref_ixml_node = p_new_node-ref_ixml_node.
  ENDIF.

  p_ref_ixml_node_parent->append_child( new_child = lo_ref_ixml_node ).

  LOOP AT p_new_node-tt_key_value_pairs INTO lv_key_value_pair.
    lo_ref_ixml_element = p_ref_ixml_document->create_element( name = lv_key_value_pair-key ).
    lo_ref_ixml_element->set_value( value = lv_key_value_pair-value ).
    lo_ref_ixml_node->append_child( new_child = lo_ref_ixml_element ).
  ENDLOOP.

ENDFORM.
```

Process result\
The result of the web service call is the PDF document in a binary stream. This stream can be converted back into PDF and for example stored on the local system. This will only work if processed in a user context as it uses the GUI\_DOWNLOAD function.

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
