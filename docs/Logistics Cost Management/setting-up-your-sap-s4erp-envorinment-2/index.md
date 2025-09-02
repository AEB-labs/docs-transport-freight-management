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

If you like to implement against the Logistics Cost Management - API from S/4Hana or SAP ERP 6.0 you have to generate one or more Enterprise services. You have to generate an Enterprise Service for each WSDL you like to use.

First, create a package from SE80. Then right click on the package choose Create -> Enterprise Services.  
Then a wizard will be shown.

![](https://files.readme.io/d332db3-2019-05-16_163832.png "2019-05-16_163832.png")

In the wizard choose Service Consumer and click on continue. Then you have to choose where source of your service is located. Choose External WSDL/Schema. Then you have to choose the data source. Here you have to choose URL. Go on with continue.  
The url you have to set is [https://rz3.aeb.de/test2billing/servlet/bf/BillingBF?WSDL](https://rz3.aeb.de/test2billing/servlet/bf/BillingBF?WSDL).  
For Logistics Cost Management this is the main API. There are some more. But for the beginning that should be enough. Go on with continue.  
Now choose the package you have created before. Set a request and leave the Prefix empty and go on with continue. Confirm the popup "No prefix entered" with enter and click on complete.  
Now the Service Consumer is created. You should see something like that:

![](https://files.readme.io/55bcecc-2019-05-17_133835.png "2019-05-17_133835.png")

## Activating Service Consumer

If that was not working please refer the the troubleshooting guide  
If there were no errors just save the Service Consumer. The next step is to activate the Service Consumer.

But one thing you have to fix first. If you check the service consumer, it will tell you that there is recursions used and that is not allowed in this context. So we have to fix that. Go to the menu -> utilities -> Settings. In the popup go to tab "Proxy Generation and there you have to mark the checkbox "Show Untyped Mapping in Proxy Editor".

![](https://files.readme.io/a6f5e5d-2019-05-17_134336.png "2019-05-17_134336.png")

Save the settings and go back to the Service Consumer. There you have to go to the "External View" Tab. Click on the binoculars and search for "record" and activate the checkbox pattern. Then on the right side you should see some details for the element "record". Click the checkbox "Untyped Mapping" and save it.

Now we can activate the service consumer. This step will generate the ABAP-Structures and ABAP-Classes what you need to implement against it. The Service consumer should now be active. If there were errors refer to the troubleshooting guide.

## Create an executable program

We have to do some steps to be able to call the webservice, but you are now able to implement something against the API. So let us do that. So that I can explain the components you will have to use if you like to call our API.  
Create an executable program and put the following code snippet into the program.

```text ABAP
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

Activate the program and execute it. The report should say "could not instantiate the billingBF". And the report tells us that there is no logical port ZBILLING_BF_TEST2 for the proxy class "ZCO_IBILLING_BF".  
But no problem we will handle that. So the next step is to create a logical port for our proxy class.  
The logical port brings the consumer service, the endpoint and the authentication data together.

## Create a logical port

Start the transaction SOAMANAGER. The SOAMANAGER will be started in an external browser window. You should like see the following.

![](https://files.readme.io/428e4fd-2019-05-16_172758.png "2019-05-16_172758.png")

You can stay on the tab Service Administration. Go to Web Service Configuration and search for our proxy class ZCO_IBILLING_BF. Just put the string ZCO_IBILLING_BF to the filter field object name and click on search.

![](https://files.readme.io/8afb351-2019-05-17_142646.png "2019-05-17_142646.png")

You should see the entry for ZCO_IBILLING_BF. Click on the blue highlighted link I marked in the screenshot. You are now on the configurations tab for ZCO_IBILLING_BF. Click on the button create and choose manual configuration. Now you see a little wizard with some steps to finish your logical port. Ok let us start.  
First you have to define the name for your logical port. Right it is the name we put in our program. So set the logical port name to ZBILLING_BF_TEST2. In the description field write whatever you want. Let the checkbox "Logical Port is Default" empty. Go on to the next step.  
You are now at step 2 "Consumer Security". Choose User ID / Password. In the field User Name you have to write "API_TEST@APITEST" (user@client) and the password in the field password. Go on to the next step. Now you have to define the HTTP Settings. Choose Complete URL and set the Url to "https://rz3.aeb.de/test2billing/servlet/bf/BillingBF". On the step SOAP Protocol set the Message ID Protocol to "Suppress ID Transfer". Then just go over the next two steps, let them with the default settings. Finally finish the configuration.

| Field name                        | Value                              | Explanation                                                                                                                  |
| :-------------------------------- | :--------------------------------- | :--------------------------------------------------------------------------------------------------------------------------- |
| URL access path                   | test2billing /servlet/bf/BillingBF | /<Pathname target system>/servlet/bf/BillingBF                                                                               |
| Computer name of access URL       | rz3.aeb.de                         | Server name of target system                                                                                                 |
| Port number of access URL         | 443                                | Port under which the target system can be accessed                                                                           |
| URL Protocol Information          | HTTPS                              | HTTP or HTTPS. To be selected according to the desired connection type.                                                      |
| Name of the proxy computer / etc. |                                    | Name of the proxy server. If a proxy must be used, enter the relevant access data for the proxy here and in the other fields |
| Compressing the HTTP message      | Active                             |                                                                                                                              |
| Compressing the response          | True                               |                                                                                                                              |

Ok now we have configured our logical port. Let us go back to our little program. Execute it.  
You will now get another error. The instance for class ZCO_IBILLING_BF could be created, but the call we wanted to do, has an error.

## Setting up the connection

The issue is that we have to import the aeb-certificates into STRUST. Then the SAP-System is allowed to communicate with rz3.aeb.de. After that the environment is set up and you can start with your business. If you run the program call should not return an error.

If you have trouble with setting up the connection refer to our communication trouble guide.