---
title: Setting up your SAP environment (LCM)
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: |-
    Problems with something in this chapter -> choose trouble shooting guide
    Otherwise start with your first service item
  pages:
    - type: basic
      slug: the-first-service-item
      title: The first service item
    - type: basic
      slug: sap-connection-trouble-shooting-lcm
      title: SAP connection trouble shooting (LCM)
    - type: basic
      slug: sap-wsdl-trouble-shooting-lcm
      title: SAP WSDL trouble shooting (LCM)
---
## Generate Enterprise Services from WSDL

To consume the Logistics Cost Management API in SAP S/4HANA or SAP ERP 6.0, you must generate one or more enterprise services. Generate one service consumer for each WSDL that you intend to use.

1. Open transaction SE80 and create a package.
2. Right-click the package and choose Create → Enterprise Services.
3. In the wizard, select Service Consumer and choose Continue.

   <Image src="https://files.readme.io/50f4fa7e2d471cd5310344b7bf20f7c29345db8b37d750a2a56412868a6e9e61-image.png" width="75%" framed={true} />

4. Select External WSDL/Schema as the service source.
5. Select URL as the data source and choose Continue.
6. Enter the following URL: [https://rz3.aeb.de/test2billing/servlet/bf/BillingBF?WSDL](https://rz3.xyz.de/test2billing/servlet/bf/BillingBF?WSDL) This WSDL represents the main API for Logistics Cost Management. Additional WSDLs are available, but this one is sufficient for the initial implementation.
7. Select the package created previously.
8. Assign a transport request.
9. Leave the Prefix field empty and choose Continue.
10. Confirm the "No prefix entered" dialog by pressing Enter, and then choose Complete.

The service consumer is now generated:


<Image src="https://files.readme.io/09cba344110e1752401dd99f31bd2ff8df2d23fd5cbb7aab7ebb07832292d6d8-image.png" framed={true} />


## Activate the Service Consumer

If the service consumer cannot be generated or activated, refer to the troubleshooting guide.

If no errors occur during generation, save the service consumer. Before activating it, however, you must adjust the proxy editor settings because the service definition contains recursive structures that are not permitted in the current context.

1. Open the service consumer.
2. Choose Utilities → Settings.
3. In the dialog box, open the Proxy Generation tab.
4. Select "Show Untyped Mapping" in Proxy Editor.

   ![](https://files.readme.io/a6f5e5d-2019-05-17_134336.png "2019-05-17_134336.png")
5. Save the settings and return to the service consumer.
6. Open the External View tab.
7. Choose the search help icon and search for "record".
8. Select the Pattern checkbox.
9. Select the record element in the results.
10. In the details area on the right, select "Untyped Mapping".
11. Save the service consumer.

You can now activate the service consumer. During activation, SAP generates the ABAP structures and classes required to consume the API.

If activation fails, refer to the troubleshooting guide.

## Create an executable program

The service consumer is now available for implementation. To test the API connection and demonstrate the required components, create an executable ABAP program and insert the provided code snippet.

```text Execute test call
DATA:
  billing_bf             TYPE REF TO zco_ibilling_bf,
  output_data            TYPE zcreate_service_items_respons1,
  input_data             TYPE zcreate_service_items1,
  system_fault_exception TYPE REF TO cx_ai_system_fault.

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


TRY.
    billing_bf->create_service_items( EXPORTING input = input_data
                                      IMPORTING output = output_data ).
  CATCH cx_ai_system_fault INTO system_fault_exception.
    WRITE 'Error when calling create service item '.
    WRITE system_fault_exception->get_text( ).
ENDTRY.
```

Activate and execute the report. The following error is expected: &#x20;

> Could not instantiate the billingBF.

The error message indicates that no logical port named ZBILLING_BF_TEST2 has been configured for the proxy class ZCO_IBILLING_BF.

The logical port configuration connects the service consumer with the endpoint and the authentication data. The next step is therefore to create a logical port for the proxy class.

## Create a logical port

1. Start transaction SOAMANAGER. The transaction opens in an external browser window.
2. Remain on the Service Administration tab.
3. Open Web Service Configuration.
4. Search for the proxy class ZCO_IBILLING_BF by entering it in the Object Name filter field.
5. Choose Search.
6. Select the entry for ZCO_IBILLING_BF.
7. Open the Configurations tab.
8. Choose Create and select Manual Configuration.
9. A wizard opens to guide you through the logical port configuration.

**Step 1: Logical Port**

1. Enter ZBILLING_BF_TEST2 as the logical port name. This name must correspond to the name specified in the ABAP program.
2. Enter an appropriate description.
3. Leave Logical Port is Default unselected.
4. Choose Next.

**Step 2: Consumer Security**

1. Select User ID / Password.
2. Enter the user name and corresponding password:  see  [Authentication](https://transport-freight-management.docs.developers.aeb.com/v2/docs/setup-your-environment-1) for more details.&#x20;
3. Choose Next.

**Step 3: HTTP Settings**

1. Select "Complete URL"
2. Enter the following URL: [https://rz3.aeb.de/test2billing/servlet/bf/BillingBF](https://rz3.xyz.de/test2billing/servlet/bf/BillingBF)
3. Choose Next.

**Step 4: SOAP Protocol**

1. Set Message ID Protocol to "Suppress ID Transfer".
2. Set Data transfer scope to "Minimal data transfer"
3. Set Transfer protocol to "Transfer via HTTP header" &#x20;

Proceed through the next two steps without changing the default settings. Finally, complete the wizard to save the logical port configuration.

## Importing certificates for HTTPS connections

Follow the instructions at [https://docs.aeb.com/doc/cm-387110283-860970507-en-US/t-860970507-391691019-en-US](https://docs.aeb.com/doc/cm-387110283-860970507-en-US/t-860970507-391691019-en-US "https://docs.aeb.com/doc/cm-387110283-860970507-en-US/t-860970507-391691019-en-US") &#x20;
