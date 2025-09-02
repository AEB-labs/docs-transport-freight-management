---
title: Setting up your SAP environment
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
## Credentials

Before you can start using the Carrier Connect API, you need a client, a user and a password. 

If you do not have those yet, you can use the following credentials to test the API.

Client: APITEST\
User: API\_TEST\
PW: API\_TEST2018

## Generate Enterprise Serivces from WSDL

If you like to implement against the Carrier Connect-API from S/4HANA or SAP ERP 6.0 you have to generate one or more Enterprise services. You have to generate an Enterprise Services for each WSDL you like to use. 

First create a package from SE80. Then right click on the package choose Create -> Enterprise Services.\
Then a wizard will be shown.  

![695](https://files.readme.io/d332db3-2019-05-16_163832.png "2019-05-16_163832.png")

In the wizard choose Service Consumer and click on continue. Then you have to choose where source of your service is located. Choose External WSDL/Schema. Then you have to choose the data source. Here you have to choose URL. Go on with continue.\
The url you have to set is [https://rz3.aeb.de/demo1cai/servlet/bf/DLCarrierBF?WSDL](https://rz3.aeb.de/demo1cai/servlet/bf/DLCarrierBF?WSDL).\
For Carrier Select this is the main API. There are some more. But for the beginning that should be sufficient. Go on with continue.\
Now choose the package you have created before. Set a request and leave the Prefix empty and go on with continue. Confirm the popup "No prefix entered" with enter and click on complete.\
Now the Service Consumer is created. You should see something like that:

![1324](https://files.readme.io/6f65189-2019-05-16_165610.png "2019-05-16_165610.png")

If that was not working please refer the the trouble shooting guide\
If there were no errors just save the Service Consumer. The next step is to activate the Service Consumer. This step will generate the ABAP-Structures and ABAP-Classes what you need to implement against it. The Service consumer should now should be active. If there were errors refer to the trouble shooting guide. 

We have to do some steps to be able to call the webservice, but you are now able to implement something against the API. So let us do that. So that i can explain the components you will have to use if you like to call our API.\
Create a executable program and put the following code snippet into the program. 

```text ABAP
DATA:
  routing_bf             TYPE REF TO zco_irouting_bf,
  output_data            TYPE zcreate_routing_task_response1,
  input_data             TYPE zcreate_routing_task1,
  system_fault_exception TYPE REF TO cx_ai_system_fault.

TRY.
    CREATE OBJECT routing_bf EXPORTING logical_port_name = 'ZROUTING_BF_TEST1'.
  CATCH cx_ai_system_fault INTO system_fault_exception.
    WRITE 'Could not instantiate the routingBF '.
    WRITE system_fault_exception->get_text( ).
    RETURN.
ENDTRY.


input_data-parameters-request-base-client_ident_code = 'APITEST'.
input_data-parameters-request-base-client_system_id = 'T23_400'.
input_data-parameters-request-base-user_name = sy-uname.


TRY.
    routing_bf->create_routing_task( EXPORTING input = input_data
                                     IMPORTING output = output_data ).
  CATCH cx_ai_system_fault into system_fault_exception.
    WRITE 'Error when calling create routing task '.
    WRITE system_fault_exception->get_text( ).
ENDTRY.
```

Activate the program and execute it. The report should say "could not instatiate the routingBF". And the report tells us that there is no logical port ZROUTING\_BF\_TEST1 for the proxy class "ZCO\_IROUTING\_BF".\
But no problem we will handle that. So the next step is to create a logical port for our proxy class.\
The logical port brings the consumer service, the endpoint and  the authenficiation data together.\
Start the transaction SOAMANAGER. The SOAMANAGER will be started in an external browser window. You should like see the following.

![1735](https://files.readme.io/428e4fd-2019-05-16_172758.png "2019-05-16_172758.png")

You can stay on the tab Service Administration. Go to Web Service Configuration and search for our proxy class ZCO\_IROUTING\_BF.  Just put the string ZCO\_IROUTING\_BF to the filter field object name and clikc on search. 

![1696](https://files.readme.io/220d760-2019-05-16_173113.png "2019-05-16_173113.png")

You should see the entry for ZCO\_IROUTING\_BF. Click on the blue highlighte link i marked in the screen shot. You are now on the Configurations tab for ZCO\_IROUTING\_BF. Click on the button create and choose manual configuration. Now you see a little wizard with some steps to finish your logical port. Ok let us start.\
First you have to define the name for your logical port. Right it is the name we put in our program. So set the logical port name to ZROUTING\_BF\_TEST1. In the description field write whatever you want. Let the checkbox "Logical Port is Default" empty. Go on to the next step.\
Your are now at step 2 "Consumer Security". Choose User ID / Password. In the field User Name you have to write "API\_TEST\@APITEST" (user\@client) and the password in the field password. Go on to the next step. Now you have to define the HTTP Settings. Choose Complete URL und set the Url to "[https://rz3.aeb.de/test1routing/servlet/bf/RoutingBF"](https://rz3.aeb.de/test1routing/servlet/bf/RoutingBF"). On the step SOAP Protocol the the Message ID Protocol to "Suppress ID Transfer". Then just got over the next two steps, let them with the default settings. Finally finish the configuration.

Ok now we have configured our logical port. Let us go back to our little programm. Execute it.\
You will now get another error.The instance for class ZCO\_IROUTING\_BF could be created, but the call we wanted to do, has an error. 

The issue is that we have to import the aeb-certficates into STRUST. Then the SAP-System is allowed to communicate with rz3.aeb.de. After that the environment is set up and you can start with your business. If you run the resport call should not return an error. 

If you have trouble with setting up the connection refer to our communitcation trouble guide.
