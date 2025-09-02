---
title: The first shipment
excerpt: Prepared calls for copy/paste in your development environment
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
      slug: common-shipping-scenarios
      title: Common shipping scenarios
---
To allow you to start quickly, you will find here a complete call to create a shipment and receive a typical response.

## Creating a shipment

You can use the example and copy/paste it into your favorite tool to test SOAP and/or REST API calls. Our test environment is prepared to work with the data in this example.\
Why don't you just give it a quick try?

```json
{
   "clientSystemId":"SOAPUI",
   "clientIdentCode":"APITEST",
   "userName":"API_TEST",
   "resultLanguageIsoCodes":[
      "EN"
   ],
   "creationParms":{
      "creationMode":"VALIDATION_OK"
   },
   "shipment":{
      "transactionId":"SHIPMENT_TEST_1",
      "transactionLabel":"SHIPMENT_TEST_1",
      "referenceNumber1":"SHIPMENT_TEST_1",
      "shippingDate":"2018-01-01",
      "contents":"SHIPMENT_CONTENT",
      "shippingPt":{
         "companyNumber":"D01",
         "initFromCompanyMasterFileData":"true"
      },
      "consignee":{
         "companyNumber":"D07",
         "name":"Max Muster",
         "initFromCompanyMasterFileData":"true"
      },
      "consigneeContact":{
         "name":"Max Muster",
         "phone":"0049123456789"
      },
      "carrierIdentCode":"DPD_DE",
      "serviceCode":"DPD_EXPR10",
      "termsOfDeliveryCode":"DDP",
      "packages":[
         {
            "packageTypeIdentCode":"BOX",
            "packageNumber":"1",
            "packageTransactionId":"PACKAGE_TEST_1",
            "referenceNumber1":"PACKAGE_TEST_1",
            "grossWeight":{
               "value":"25",
               "unit":"kg"
            }
         }
      ]
   },
   "processParms":{
      "processMode":{
         "mode":"EXTENDED"
      },
      "documentPrepareScope":{
         "scope":"ALL"
      },
      "workstationId":"PDF_WORKSTATION",
      "documentOutputScope":{
         "scope":"ALL"
      },
      "documentOutputMode":{
         "mode":"RETURN"
      },
      "doCompletion":"true"
   }
}
```
```xml
<createShipment>
   <request>
      <clientSystemId>SOAPUI</clientSystemId>
      <clientIdentCode>APITEST</clientIdentCode>
      <userName>API_TEST</userName>
      <resultLanguageIsoCodes>EN</resultLanguageIsoCodes>
      <creationParms>
         <creationMode>VALIDATION_OK</creationMode>
      </creationParms>
      <shipment>
         <transactionId>SHIPMENT_TEST_1</transactionId>
         <transactionLabel>SHIPMENT_TEST_1</transactionLabel>
         <referenceNumber1>SHIPMENT_TEST_1</referenceNumber1>
         <shippingDate>2018-01-01</shippingDate>
         <contents>SHIPMENT_CONTENT</contents>
         <shippingPt>
            <companyNumber>D01</companyNumber>
            <initFromCompanyMasterFileData>true</initFromCompanyMasterFileData>
         </shippingPt>
         <consignee>
            <companyNumber>D07</companyNumber>
            <name>Max Muster</name>
            <initFromCompanyMasterFileData>true</initFromCompanyMasterFileData>
         </consignee>
         <consigneeContact>
            <name>Max Muster</name>
            <phone>0049123456789</phone>
         </consigneeContact>
         <carrierIdentCode>DPD_DE</carrierIdentCode>
         <serviceCode>DPD_EXPR10</serviceCode>
         <termsOfDeliveryCode>DDP</termsOfDeliveryCode>
         <packages>
            <packageTypeIdentCode>BOX</packageTypeIdentCode>
            <packageNumber>1</packageNumber>
            <packageTransactionId>PACKAGE_TEST_1</packageTransactionId>
            <referenceNumber1>PACKAGE_TEST_1</referenceNumber1>
            <grossWeight>
               <value>25</value>
               <unit>kg</unit>
            </grossWeight>
         </packages>
      </shipment>
      <processParms>
         <processMode>
            <mode>EXTENDED</mode>
         </processMode>
         <documentPrepareScope>
            <scope>ALL</scope>
         </documentPrepareScope>
         <workstationId>PDF_WORKSTATION</workstationId>
         <documentOutputScope>
            <scope>ALL</scope>
         </documentOutputScope>
         <documentOutputMode>
            <mode>RETURN</mode>
         </documentOutputMode>
         <doCompletion>true</doCompletion>
      </processParms>
   </request>
</createShipment>
```

## Receiving an error

Below is an API call which will return an error. This will demonstrate the structure of an error response and will allow you to become familiar with the general behavior.\
You will receive this message once you remove *clientSystemId* from the above request.

```json
{
   "hasErrors":"true",
   "hasOnlyRetryableErrors":"false",
   "hasWarnings":"false",
   "messages":{
      "messageType":"ERROR",
      "messageIdentCode":"EMPTY_MANDATORY_FIELD",
      "messageTexts":{
         "languageISOCode":"en",
         "text":"Client system id not filled."
      },
      "indentationLevel":"0"
   }
}
```
```xml
<createShipmentResponse>
   <result>
      <hasErrors>true</hasErrors>
      <hasOnlyRetryableErrors>false</hasOnlyRetryableErrors>
      <hasWarnings>false</hasWarnings>
      <messages>
         <messageType>ERROR</messageType>
         <messageIdentCode>EMPTY_MANDATORY_FIELD</messageIdentCode>
         <messageTexts>
            <languageISOCode>en</languageISOCode>
            <text>Client system id not filled.</text>
         </messageTexts>
         <indentationLevel>0</indentationLevel>
      </messages>
   </result>
</createShipmentResponse>
```
