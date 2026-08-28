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
## Credentials

Before you can start using the API, you need a user and a password. See [Authentication](https://transport-freight-management.docs.developers.aeb.com/v2/docs/setup-your-environment-1) for more details.

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

<br />

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

Start the transaction SOAMANAGER. The SOAMANAGER will be started in an external browser window. You should like see the following.

![](https://files.readme.io/428e4fd-2019-05-16_172758.png "2019-05-16_172758.png")

You can stay on the tab Service Administration. Go to Web Service Configuration and search for our proxy class ZCO_IBILLING_BF. Just put the string ZCO_IBILLING_BF to the filter field object name and click on search.

![](https://files.readme.io/8afb351-2019-05-17_142646.png "2019-05-17_142646.png")

You should see the entry for ZCO_IBILLING_BF. Click on the blue highlighted link I marked in the screenshot. You are now on the configurations tab for ZCO_IBILLING_BF. Click on the button create and choose manual configuration. Now you see a little wizard with some steps to finish your logical port. Ok let us start.<br />First you have to define the name for your logical port. Right it is the name we put in our program. So set the logical port name to ZBILLING_BF_TEST2. In the description field write whatever you want. Let the checkbox "Logical Port is Default" empty. Go on to the next step.<br />You are now at step 2 "Consumer Security". Choose User ID / Password. In the field User Name you have to write "API_TEST\@APITEST" (user\@client) and the password in the field password. Go on to the next step. Now you have to define the HTTP Settings. Choose Complete URL and set the Url to "[https://rz3.aeb.de/test2billing/servlet/bf/BillingBF](https://rz3.aeb.de/test2billing/servlet/bf/BillingBF)". On the step SOAP Protocol set the Message ID Protocol to "Suppress ID Transfer". Then just go over the next two steps, let them with the default settings. Finally finish the configuration.

| Field name                        | Value                              | Explanation                                                                                                                  |
| :-------------------------------- | :--------------------------------- | :--------------------------------------------------------------------------------------------------------------------------- |
| URL access path                   | test2billing /servlet/bf/BillingBF | `<Pathname target system>`/servlet/bf/BillingBF                                                                              |
| Computer name of access URL       | rz3.aeb.de                         | Server name of target system                                                                                                 |
| Port number of access URL         | 443                                | Port under which the target system can be accessed                                                                           |
| URL Protocol Information          | HTTPS                              | HTTP or HTTPS. To be selected according to the desired connection type.                                                      |
| Name of the proxy computer / etc. |                                    | Name of the proxy server. If a proxy must be used, enter the relevant access data for the proxy here and in the other fields |
| Compressing the HTTP message      | Active                             |                                                                                                                              |
| Compressing the response          | True                               |                                                                                                                              |

Ok now we have configured our logical port. Let us go back to our little program. Execute it.<br />You will now get another error. The instance for class ZCO_IBILLING_BF could be created, but the call we wanted to do, has an error.

## Setting up the connection

The issue is that we have to import the aeb-certificates into STRUST. Then the SAP-System is allowed to communicate with rz3.aeb.de. After that the environment is set up and you can start with your business. If you run the program call should not return an error.

If you have trouble with setting up the connection refer to our communication trouble guide.
