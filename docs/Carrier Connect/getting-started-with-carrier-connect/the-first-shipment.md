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

##Creating a shipment
You can use the example and copy/paste it into your favorite tool to test SOAP and/or REST API calls. Our test environment is prepared to work with the data in this example.
Why don't you just give it a quick try?
[block:code]
{
  "codes": [
    {
      "code": "{\n   \"clientSystemId\":\"SOAPUI\",\n   \"clientIdentCode\":\"APITEST\",\n   \"userName\":\"API_TEST\",\n   \"resultLanguageIsoCodes\":[\n      \"EN\"\n   ],\n   \"creationParms\":{\n      \"creationMode\":\"VALIDATION_OK\"\n   },\n   \"shipment\":{\n      \"transactionId\":\"SHIPMENT_TEST_1\",\n      \"transactionLabel\":\"SHIPMENT_TEST_1\",\n      \"referenceNumber1\":\"SHIPMENT_TEST_1\",\n      \"shippingDate\":\"2018-01-01\",\n      \"contents\":\"SHIPMENT_CONTENT\",\n      \"shippingPt\":{\n         \"companyNumber\":\"D01\",\n         \"initFromCompanyMasterFileData\":\"true\"\n      },\n      \"consignee\":{\n         \"companyNumber\":\"D07\",\n         \"name\":\"Max Muster\",\n         \"initFromCompanyMasterFileData\":\"true\"\n      },\n      \"consigneeContact\":{\n         \"name\":\"Max Muster\",\n         \"phone\":\"0049123456789\"\n      },\n      \"carrierIdentCode\":\"DPD_DE\",\n      \"serviceCode\":\"DPD_EXPR10\",\n      \"termsOfDeliveryCode\":\"DDP\",\n      \"packages\":[\n         {\n            \"packageTypeIdentCode\":\"BOX\",\n            \"packageNumber\":\"1\",\n            \"packageTransactionId\":\"PACKAGE_TEST_1\",\n            \"referenceNumber1\":\"PACKAGE_TEST_1\",\n            \"grossWeight\":{\n               \"value\":\"25\",\n               \"unit\":\"kg\"\n            }\n         }\n      ]\n   },\n   \"processParms\":{\n      \"processMode\":{\n         \"mode\":\"EXTENDED\"\n      },\n      \"documentPrepareScope\":{\n         \"scope\":\"ALL\"\n      },\n      \"workstationId\":\"PDF_WORKSTATION\",\n      \"documentOutputScope\":{\n         \"scope\":\"ALL\"\n      },\n      \"documentOutputMode\":{\n         \"mode\":\"RETURN\"\n      },\n      \"doCompletion\":\"true\"\n   }\n}",
      "language": "json"
    },
    {
      "code": "<createShipment>\n   <request>\n      <clientSystemId>SOAPUI</clientSystemId>\n      <clientIdentCode>APITEST</clientIdentCode>\n      <userName>API_TEST</userName>\n      <resultLanguageIsoCodes>EN</resultLanguageIsoCodes>\n      <creationParms>\n         <creationMode>VALIDATION_OK</creationMode>\n      </creationParms>\n      <shipment>\n         <transactionId>SHIPMENT_TEST_1</transactionId>\n         <transactionLabel>SHIPMENT_TEST_1</transactionLabel>\n         <referenceNumber1>SHIPMENT_TEST_1</referenceNumber1>\n         <shippingDate>2018-01-01</shippingDate>\n         <contents>SHIPMENT_CONTENT</contents>\n         <shippingPt>\n            <companyNumber>D01</companyNumber>\n            <initFromCompanyMasterFileData>true</initFromCompanyMasterFileData>\n         </shippingPt>\n         <consignee>\n            <companyNumber>D07</companyNumber>\n            <name>Max Muster</name>\n            <initFromCompanyMasterFileData>true</initFromCompanyMasterFileData>\n         </consignee>\n         <consigneeContact>\n            <name>Max Muster</name>\n            <phone>0049123456789</phone>\n         </consigneeContact>\n         <carrierIdentCode>DPD_DE</carrierIdentCode>\n         <serviceCode>DPD_EXPR10</serviceCode>\n         <termsOfDeliveryCode>DDP</termsOfDeliveryCode>\n         <packages>\n            <packageTypeIdentCode>BOX</packageTypeIdentCode>\n            <packageNumber>1</packageNumber>\n            <packageTransactionId>PACKAGE_TEST_1</packageTransactionId>\n            <referenceNumber1>PACKAGE_TEST_1</referenceNumber1>\n            <grossWeight>\n               <value>25</value>\n               <unit>kg</unit>\n            </grossWeight>\n         </packages>\n      </shipment>\n      <processParms>\n         <processMode>\n            <mode>EXTENDED</mode>\n         </processMode>\n         <documentPrepareScope>\n            <scope>ALL</scope>\n         </documentPrepareScope>\n         <workstationId>PDF_WORKSTATION</workstationId>\n         <documentOutputScope>\n            <scope>ALL</scope>\n         </documentOutputScope>\n         <documentOutputMode>\n            <mode>RETURN</mode>\n         </documentOutputMode>\n         <doCompletion>true</doCompletion>\n      </processParms>\n   </request>\n</createShipment>",
      "language": "xml"
    }
  ]
}
[/block]
##Receiving an error
Below is an API call which will return an error. This will demonstrate the structure of an error response and will allow you to become familiar with the general behavior.
You will receive this message once you remove *clientSystemId* from the above request.
[block:code]
{
  "codes": [
    {
      "code": "{\n   \"hasErrors\":\"true\",\n   \"hasOnlyRetryableErrors\":\"false\",\n   \"hasWarnings\":\"false\",\n   \"messages\":{\n      \"messageType\":\"ERROR\",\n      \"messageIdentCode\":\"EMPTY_MANDATORY_FIELD\",\n      \"messageTexts\":{\n         \"languageISOCode\":\"en\",\n         \"text\":\"Client system id not filled.\"\n      },\n      \"indentationLevel\":\"0\"\n   }\n}",
      "language": "json"
    },
    {
      "code": "<createShipmentResponse>\n   <result>\n      <hasErrors>true</hasErrors>\n      <hasOnlyRetryableErrors>false</hasOnlyRetryableErrors>\n      <hasWarnings>false</hasWarnings>\n      <messages>\n         <messageType>ERROR</messageType>\n         <messageIdentCode>EMPTY_MANDATORY_FIELD</messageIdentCode>\n         <messageTexts>\n            <languageISOCode>en</languageISOCode>\n            <text>Client system id not filled.</text>\n         </messageTexts>\n         <indentationLevel>0</indentationLevel>\n      </messages>\n   </result>\n</createShipmentResponse>",
      "language": "xml"
    }
  ]
}
[/block]