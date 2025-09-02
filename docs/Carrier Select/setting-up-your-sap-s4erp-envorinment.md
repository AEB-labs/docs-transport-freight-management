---
title: Setting up your SAP environment
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
    Otherwise start with your first routing task.
  pages:
    - type: basic
      slug: the-first-routing-task
      title: The first routing task
    - type: basic
      slug: s4-hana-erp-connection-trouble-shooting
      title: SAP connection trouble shooting
    - type: basic
      slug: s4-hana-erp-issues-with-importing-wsdl
      title: SAP WSDL trouble shooting
---
## Credentials
Before you can start using the Carrier Connect API, you need a client, a user and a password. 

If you do not have those yet, you can use the following credentials to test the API.

Client: APITEST
User: API_TEST
PW: API_TEST2018

## Generate Enterprise Serivces from WSDL 
If you like to implement against the CarrierSelect-API from S/4Hana or SAP ERP 6.0 you have to generate one or more Enterprise services. You have to generate an Enterprise Services for each WSDL you like to use. 

First create a package from SE80. Then right click on the package choose Create -> Enterprise Services. 
Then a wizard will be shown.  
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d332db3-2019-05-16_163832.png",
        "2019-05-16_163832.png",
        695,
        551,
        "#b6c7d3"
      ]
    }
  ]
}
[/block]
In the wizard choose Service Consumer and click on continue. Then you have to choose where source of your service is located. Choose External WSDL/Schema. Then you have to choose the data source. Here you have to choose URL. Go on with continue. 
The url you have to set is https://rz3.aeb.de/test2routing/servlet/bf/RoutingBF?WSDL.
For Carrier Select this is the main API. There are some more. But for the beginning that should be enough. Go on with continue. 
Now choose the package you have created before. Set a request and leave the Prefix empty and go on with continue. Confirm the popup "No prefix entered" with enter and click on complete. 
Now the Service Consumer is created. You should see something like that:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6f65189-2019-05-16_165610.png",
        "2019-05-16_165610.png",
        1324,
        639,
        "#dce5ec"
      ]
    }
  ]
}
[/block]
If that was not working please refer the the trouble shooting guide 
If there were no errors just save the Service Consumer. The next step is to activate the Service Consumer. This step will generate the ABAP-Structures and ABAP-Classes what you need to implement against it. The Service consumer should now should be active. If there were errors refer to the trouble shooting guide. 

We have to do some steps to be able to call the webservice, but you are now able to implement something against the API. So let us do that. So that i can explain the components you will have to use if you like to call our API. 
Create a executable program and put the following code snippet into the program. 
[block:code]
{
  "codes": [
    {
      "code": "DATA:\n  routing_bf             TYPE REF TO zco_irouting_bf,\n  output_data            TYPE zcreate_routing_task_response1,\n  input_data             TYPE zcreate_routing_task1,\n  system_fault_exception TYPE REF TO cx_ai_system_fault.\n\nTRY.\n    CREATE OBJECT routing_bf EXPORTING logical_port_name = 'ZROUTING_BF_TEST1'.\n  CATCH cx_ai_system_fault INTO system_fault_exception.\n    WRITE 'Could not instantiate the routingBF '.\n    WRITE system_fault_exception->get_text( ).\n    RETURN.\nENDTRY.\n\n\ninput_data-parameters-request-base-client_ident_code = 'APITEST'.\ninput_data-parameters-request-base-client_system_id = 'T23_400'.\ninput_data-parameters-request-base-user_name = sy-uname.\n\n\nTRY.\n    routing_bf->create_routing_task( EXPORTING input = input_data\n                                     IMPORTING output = output_data ).\n  CATCH cx_ai_system_fault into system_fault_exception.\n    WRITE 'Error when calling create routing task '.\n    WRITE system_fault_exception->get_text( ).\nENDTRY.",
      "language": "text",
      "name": "ABAP"
    }
  ]
}
[/block]
Activate the program and execute it. The report should say "could not instatiate the routingBF". And the report tells us that there is no logical port ZROUTING_BF_TEST1 for the proxy class "ZCO_IROUTING_BF". 
But no problem we will handle that. So the next step is to create a logical port for our proxy class. 
The logical port brings the consumer service, the endpoint and  the authenficiation data together. 
Start the transaction SOAMANAGER. The SOAMANAGER will be started in an external browser window. You should like see the following.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/428e4fd-2019-05-16_172758.png",
        "2019-05-16_172758.png",
        1735,
        664,
        "#eaf1f4"
      ]
    }
  ]
}
[/block]
You can stay on the tab Service Administration. Go to Web Service Configuration and search for our proxy class ZCO_IROUTING_BF.  Just put the string ZCO_IROUTING_BF to the filter field object name and clikc on search. 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/220d760-2019-05-16_173113.png",
        "2019-05-16_173113.png",
        1696,
        631,
        "#f1f6f7"
      ]
    }
  ]
}
[/block]
You should see the entry for ZCO_IROUTING_BF. Click on the blue highlighte link i marked in the screen shot. You are now on the Configurations tab for ZCO_IROUTING_BF. Click on the button create and choose manual configuration. Now you see a little wizard with some steps to finish your logical port. Ok let us start. 
First you have to define the name for your logical port. Right it is the name we put in our program. So set the logical port name to ZROUTING_BF_TEST1. In the description field write whatever you want. Let the checkbox "Logical Port is Default" empty. Go on to the next step. 
Your are now at step 2 "Consumer Security". Choose User ID / Password. In the field User Name you have to write "API_TEST@APITEST" (user@client) and the password in the field password. Go on to the next step. Now you have to define the HTTP Settings. Choose Complete URL und set the Url to "https://rz3.aeb.de/test1routing/servlet/bf/RoutingBF". On the step SOAP Protocol the the Message ID Protocol to "Suppress ID Transfer". Then just got over the next two steps, let them with the default settings. Finally finish the configuration.

Ok now we have configured our logical port. Let us go back to our little programm. Execute it. 
You will now get another error.The instance for class ZCO_IROUTING_BF could be created, but the call we wanted to do, has an error. 

The issue is that we have to import the aeb-certficates into STRUST. Then the SAP-System is allowed to communicate with rz3.aeb.de. After that the environment is set up and you can start with your business. If you run the resport call should not return an error. 

If you have trouble with setting up the connection refer to our communitcation trouble guide.