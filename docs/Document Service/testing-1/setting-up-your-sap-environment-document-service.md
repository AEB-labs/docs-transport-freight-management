---
title: Setting up your SAP environment (Document Service)
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
  pages:
    - type: basic
      slug: creation-of-the-first-document
      title: Creation of the first document
---
## Credentials
Before you can start using the Document Service API, you need a client, a user and a password. 
For testing you can use:
https://rz3.aeb.de/demo1docs/
Mandant(client): APITEST
User: API_TEST
PW: API_TEST2021

## Generate Enterprise Services from WSDL 
If you like to implement against the Document Service - API from S/4Hana or SAP ERP 6.0 you have to generate one or more Enterprise services. You have to generate an Enterprise Services for each WSDL you like to use. 

First create a package from SE80. Then right click on the package choose Create -> Enterprise Services. 
Then a wizard will be shown.  
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/25143a5-2021-04-29_170938.png",
        "2021-04-29_170938.png",
        691,
        544,
        "#c1cacb"
      ]
    }
  ]
}
[/block]
In the wizard choose Service Consumer and click on continue. Then you have to choose where the source of your service is located. Choose External WSDL/Schema. Then you have to choose the data source. Here you have to choose URL. Go on with continue. 
The URL you have to set is https://rz3.aeb.de/test2docs/servlet/bf/DocumentServiceBF?WSDL.
It's recommended to download the WSDL first and do a local upload from file. Please also keep in mind to download the corresponding XSD.
Now choose the package you have created before. Set a request and provide a Prefix if necessary and go on with continue. 
Now the Service Consumer is created. You should see something like that:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2796c7f-2021-04-29_171525.png",
        "2021-04-29_171525.png",
        1311,
        481,
        "#ebded3"
      ]
    }
  ]
}
[/block]
## Activating Service Consumer
If that was not working please refer the the trouble shooting guide.
If there were no errors just save the Service Consumer. The next step is to activate the Service Consumer. 
If you check the service consumer, it will tell you that there are recursions used and that is not allowed in this context. So we have to fix that. Go to the menu -> utilities -> Settings. In the popup go to tab "Proxy Generation and there you have to mark the checkbox "Show Untyped Mapping in Proxy Editor". 
Save the settings and go back to the Service Consumer. There you have to go to the "External View" Tab. Click on the binoculars and search for "record" and activate the checkbox pattern. Then on the right side you should see some details for the element "record". Click the checkbox "Untyped Mapping" and save it. 
Alternatively you can remove the recursive segments already in the XSD before it's uploaded to SAP.

Now the service consumer can be activated. This step will generate the ABAP-Structures and ABAP-Classes what you need to implement against it. The Service consumer should now be active. If there were errors refer to the trouble shooting guide. 

## Create an executable program
It's now possible to implement something against the API.  
Create an executable program and put the following code snippet into the program. 
[block:code]
{
  "codes": [
    {
      "code": "DATA:\n  document_service_bf    TYPE REF TO zco_idocument_service_bf,\n  output_data            TYPE zcreate_document_response1,\n  input_data             TYPE zcreate_document1,\n  system_fault_exception TYPE REF TO cx_ai_system_fault,\n  soap_fault_excepton    TYPE REF TO cx_ai_soap_fault.\n\n\"Instatiate BF\nTRY.\n    CREATE OBJECT document_service_bf EXPORTING logical_port_name = 'ZDOCUMENT_SERVICE_BF_TEST'.\n  CATCH cx_ai_system_fault INTO system_fault_exception.\n    WRITE 'Could not instantiate the document_bf'.\n    WRITE system_fault_exception->get_text( ).\n    RETURN.\nENDTRY.\n\n\"Execute BF call\nTRY.\n    document_service_bf->create_document( EXPORTING  input = input_data\n                           IMPORTING output = output_data ).\n\n  CATCH cx_ai_soap_fault INTO soap_fault_excepton.\n    WRITE soap_fault_excepton->get_text( ).\n  CATCH cx_ai_system_fault INTO system_fault_exception.\n    WRITE system_fault_exception->get_text( ).\nENDTRY. ",
      "language": "text"
    }
  ]
}
[/block]
Activate the program and execute it. The report should say "could not instatiate the billingBF". And the report tells us that there is no logical port ZAEB_DOCUMENT_SERVICE for the proxy class "ZAEB_DOCSCO_IDOCUMENT_SERVICE". 
The next step is to create a logical port for our proxy class. 
The logical port brings the consumer service, the endpoint and  the authenficiation data together. 

##Import certificates to STRUST
To enable a direct HTTPS connection between the SAP system and the AEB data center, you need the ‘Root-SSL’ and ‘Intermediate’ certificates issued by AEB. You can open the required certificates in the Chrome browser using the following links and save them locally as a file.
1.	EV Root:
https://www.digicert.com/CACerts/DigiCertHighAssuranceEVRootCA.crt 
2.	EV Intermediate:
https://www.digicert.com/CACerts/DigiCertSHA2ExtendedValidationServerCA.crt 
3.	Non-EV Root:
https://www.digicert.com/CACerts/DigiCertGlobalRootCA.crt 
4.	Non-EV Intermediate:
https://www.digicert.com/CACerts/DigiCertSHA2SecureServerCA.crt 
Alternatively, you can also download the certificates from https://www.digicert.com/digicert-root-certificates.htm. Search there for the following names:
-	DigiCert High Assurance EV Root CA
-	DigiCert SHA2 Extendded Validation Server CA
-	DigiCertGlobal Root CA
-	DigiCert SHA2 Secure Server CA
Proceed as follows to import the certificates into the SAP system:
1.	To install the certificates, start the transaction STRUST.
2.	Double-click on SSL CLIENT (default). For setup via the SOAMANAGER, the certificates must also be loaded into the SSL CLIENT (anonymous).
3.	In the Certificate field group, click the Import certificate button.
4.	In the window that opens, select binary for the File format option.
5.	Select the appropriate file with the certificate for import.
6.	Next, click Add to certificate list.
7.	Go to the PSE menu and select Distribute All. 
 	The certificate is now distributed and installed on all application servers.
8.	To update the imported certificates in the ICM, start the transaction SMICM, go to the Administration menu, and select ICM – Exit Soft – Global.


##Create a logical port
Start the transaction SOAMANAGER. The SOAMANAGER will be started in an external browser window. You should like see the following.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e6a2ce0-2021-04-29_172537.png",
        "2021-04-29_172537.png",
        1426,
        630,
        "#e9ecef"
      ]
    }
  ]
}
[/block]
Go to Web Service Configuration and search for your proxy class ZAEB_DOCSCO_IDOCUMENT_SERVICE.  
Configuring a logical port with SOMANAGER (SAP NetWeaver Release 7.1 and higher)
- Start the transaction SOAMANAGER.
- Click the Web service configuration link.
- Select Object type as the search criterion and enter the search term Consumer proxy.
- Select Object name as the second search criterion and enter the search term  IDocumentServiceBF.
Click Search. In the list of search results, the consumer proxy with the internal name ZAEB_DOCSCO_IDOCUMENT_SERVICE and the name  IDocumentServiceBF is displayed.
- In the entry, click on the link in the Internal name column.
- In the consumer proxy details displayed below, select the Configurations sheet and click Create – Manual configuration.
- Enter a name of your choice for the logical port and its description, then click the Next.
- In the Consumer security sheet, select the User ID and password option for an HTTPS connection, i.e. for all connections to the AEB data center. Specify the user ID in the format of <user in the target system>@<client of the target system> and the password matching the user.
When you are finished, click Next.
- In the HTTP settings step, enter the following values:
[block:parameters]
{
  "data": {
    "h-0": "Field name",
    "h-1": "Value",
    "h-2": "Explanation",
    "0-0": "Log",
    "0-1": "HTTPS",
    "0-2": "",
    "1-0": "Host",
    "1-1": "rz3.aeb.de",
    "1-2": "Server name of target system",
    "2-0": "Port",
    "2-1": "443",
    "2-2": "Port under which the target system can be accessed",
    "3-0": "Path",
    "3-1": "/test2docs/servlet/bf/DocumentServiceBF",
    "3-2": "Ask your AEB representative if you do not know the path name of the target system.",
    "4-0": "Name of the proxy computer / etc.",
    "4-2": "If a proxy must be used, enter the relevant access data for the proxy here and in the other fields",
    "5-0": "Execute local call",
    "5-1": "No local system call",
    "6-0": "Transport binding type",
    "6-1": "SOAP 1.1",
    "4-1": "Name of the proxy server",
    "7-0": "Max. waiting time WS consumer",
    "7-1": "0",
    "8-0": "Optimized XML transfer",
    "8-1": "none",
    "9-0": "Compressing the HTTP message",
    "9-1": "Active",
    "10-0": "Compressing the response",
    "10-1": "True"
  },
  "cols": 3,
  "rows": 11
}
[/block]
When you are finished, click Next. In the SOAP log step, enter the following values:
[block:parameters]
{
  "data": {
    "h-0": "Field name",
    "h-1": "Value",
    "0-0": "Message ID log:",
    "0-1": "Suppress ID transfer",
    "1-0": "Scope of data transfer",
    "1-1": "Minimal data transfer",
    "2-0": "Transfer log",
    "2-1": "Transfer via HTTP header"
  },
  "cols": 2,
  "rows": 3
}
[/block]
Click Finished to save the configuration of the logical port. The logical port should be displayed with the Active status in the list of logical ports for the consumer proxy. Otherwise, activate the port manually using the Activate button.