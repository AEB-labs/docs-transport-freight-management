---
title: Common shipping scenarios
excerpt: Find out what's best for you
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
      slug: steering-workflow-data-preparation-and-printing
      title: Steering workflow, data preparation, and printing
---
From many years of experience in enabling our customers to seamlessly integrate their shipping processes with any carrier, we know that there is not only one possible process but many.

We have prepared information to assist you in integrating your processes with a very flexible API which covers simple as well as more complex shipping scenarios in an easy and homogeneous way.

Below, you will find some of the most common scenarios and how you can implement them using our API.
[block:callout]
{
  "type": "info",
  "title": "Keeping data and documents right",
  "body": "**Due to the various shipping scenarios our customers are faced with, Carrier Connect provides maximum flexibility in its API.** However, this means that you have to keep in mind that after you've started printing documents all following changes might alter the data printed on the documents. It is your responsibility to make sure that no negative consequences on your processes and the carriers' operational processes result from these subsequent changes."
}
[/block]
##Shipping with only one API call
In some cases, processes allow that all shipping data are available and finalized. No changes are expected anymore.
This provides an easy context and makes it possible to ship by just sending one API call. With this one call you can create the shipment, include packages and items, complete the shipment, and request that documents should be returned in the response.

**An example with one package:**
[block:code]
{
  "codes": [
    {
      "code": "{\n   \"clientSystemId\":\"SOAPUI\",\n   \"clientIdentCode\":\"APITEST\",\n   \"userName\":\"API_TEST\",\n   \"resultLanguageIsoCodes\":[\n      \"EN\"\n   ],\n   \"creationParms\":{\n      \"creationMode\":\"VALIDATION_OK\"\n   },\n   \"shipment\":{\n      \"transactionId\":\"SHIPMENT_TEST_1\",\n      \"transactionLabel\":\"SHIPMENT_TEST_1\",\n      \"isDocumentShipment\":\"false\",\n      \"referenceNumber1\":\"SHIPMENT_TEST_1\",\n      \"shippingDate\":\"2018-01-01\",\n      \"contents\":\"SHIPMENT_CONTENT\",\n      \"shippingPt\":{\n         \"companyNumber\":\"SHIP_COMPANY_1\",\n         \"name\":\"AEB Shipping Point\",\n         \"street\":\"AEB Street 1\",\n         \"postcode\":\"70567\",\n         \"city\":\"Stuttgart\",\n         \"countryISOCode\":\"DE\",\n         \"initFromCompanyMasterFileData\":\"false\"\n      },\n      \"shippingPtContact\":{\n         \"name\":\"Peter Maier\",\n         \"phone\":\"0049711728420\"\n      },\n      \"consignee\":{\n         \"companyNumber\":\"CONSIGNEE_COMPANY_1\",\n         \"name\":\"Max Muster\",\n         \"street\":\"Muster Street 1\",\n         \"postcode\":\"10555\",\n         \"city\":\"Berlin\",\n         \"countryISOCode\":\"DE\",\n         \"initFromCompanyMasterFileData\":\"false\"\n      },\n      \"consigneeContact\":{\n         \"name\":\"Max Muster\",\n         \"phone\":\"0049123456789\"\n      },\n      \"carrierIdentCode\":\"DPD_DE\",\n      \"serviceCode\":\"DPD_EXPR10\",\n      \"termsOfDeliveryCode\":\"DDP\",\n      \"packages\":[\n         {\n            \"packageTypeIdentCode\":\"BOX\",\n            \"packageNumber\":\"1\",\n            \"packageTransactionId\":\"PACKAGE_TEST_1\",\n            \"referenceNumber1\":\"PACKAGE_TEST_1\",\n            \"grossWeight\":{\n               \"value\":\"25\",\n               \"unit\":\"kg\"\n            }\n         }\n      ]\n   },\n   \"processParms\":{\n      \"processMode\":{\n         \"mode\":\"EXTENDED\"\n      },\n      \"documentPrepareScope\":{\n         \"scope\":\"ALL\"\n      },\n      \"workstationId\":\"PDF_WORKSTATION\",\n      \"documentOutputScope\":{\n         \"scope\":\"ALL\"\n      },\n      \"documentOutputMode\":{\n         \"mode\":\"RETURN\"\n      },\n      \"doCompletion\":\"true\"\n   }\n}",
      "language": "json"
    },
    {
      "code": "<createShipment>\n   <request>\n      <clientSystemId>SOAPUI</clientSystemId>\n      <clientIdentCode>APITEST</clientIdentCode>\n      <userName>API_TEST</userName>\n      <resultLanguageIsoCodes>EN</resultLanguageIsoCodes>\n      <creationParms>\n         <creationMode>VALIDATION_OK</creationMode>\n      </creationParms>\n      <shipment>\n         <transactionId>SHIPMENT_TEST_1</transactionId>\n         <transactionLabel>SHIPMENT_TEST_1</transactionLabel>\n         <isDocumentShipment>false</isDocumentShipment>\n         <referenceNumber1>SHIPMENT_TEST_1</referenceNumber1>\n         <shippingDate>2018-01-01</shippingDate>\n         <contents>SHIPMENT_CONTENT</contents>\n         <shippingPt>\n            <companyNumber>SHIP_COMPANY_1</companyNumber>\n            <name>AEB Shipping Point</name>\n            <street>AEB Street 1</street>\n            <postcode>70567</postcode>\n            <city>Stuttgart</city>\n            <countryISOCode>DE</countryISOCode>\n            <initFromCompanyMasterFileData>false</initFromCompanyMasterFileData>\n         </shippingPt>\n         <shippingPtContact>\n            <name>Peter Maier</name>\n            <phone>0049711728420</phone>\n         </shippingPtContact>\n         <consignee>\n            <companyNumber>CONSIGNEE_COMPANY_1</companyNumber>\n            <name>Max Muster</name>\n            <street>Muster Street 1</street>\n            <postcode>10555</postcode>\n            <city>Berlin</city>\n            <countryISOCode>DE</countryISOCode>\n            <initFromCompanyMasterFileData>false</initFromCompanyMasterFileData>\n         </consignee>\n         <consigneeContact>\n            <name>Max Muster</name>\n            <phone>0049123456789</phone>\n         </consigneeContact>\n         <carrierIdentCode>DPD_DE</carrierIdentCode>\n         <serviceCode>DPD_EXPR10</serviceCode>\n         <termsOfDeliveryCode>DDP</termsOfDeliveryCode>\n         <packages>\n            <packageTypeIdentCode>BOX</packageTypeIdentCode>\n            <packageNumber>1</packageNumber>\n            <packageTransactionId>PACKAGE_TEST_1</packageTransactionId>\n            <referenceNumber1>PACKAGE_TEST_1</referenceNumber1>\n            <grossWeight>\n               <value>25</value>\n               <unit>kg</unit>\n            </grossWeight>\n         </packages>\n      </shipment>\n      <processParms>\n         <processMode>\n            <mode>EXTENDED</mode>\n         </processMode>\n         <documentPrepareScope>\n            <scope>ALL</scope>\n         </documentPrepareScope>\n         <workstationId>PDF_WORKSTATION</workstationId>\n         <documentOutputScope>\n            <scope>ALL</scope>\n         </documentOutputScope>\n         <documentOutputMode>\n            <mode>RETURN</mode>\n         </documentOutputMode>\n         <doCompletion>true</doCompletion>\n      </processParms>\n   </request>\n</createShipment>",
      "language": "xml",
      "name": ""
    }
  ]
}
[/block]
**API Response to the above call**
[block:code]
{
  "codes": [
    {
      "code": "{\n   \"hasErrors\":\"false\",\n   \"hasOnlyRetryableErrors\":\"false\",\n   \"hasWarnings\":\"false\",\n   \"shipmentNumber\":\"0000005\",\n   \"carrierShipmentNumber\":\"00000000000000\",\n   \"packageResults\":{\n      \"packageTransactionId\":\"PACKAGE_TEST_1\",\n      \"referenceNumber1\":\"PACKAGE_TEST_1\",\n      \"carrierPackageNumber\":\"00000000000000\",\n      \"documents\":{\n         \"documentType\":\"DPD Label DE\",\n         \"mimeType\":\"application/pdf\",\n         \"content\":\"PDF Content in Base64 encoded\"\n      }\n   },\n   \"accountInfo\":{\n      \"customerNumberAtCarrier\":\"1234567890\",\n      \"singlePackageHandlingActivated\":\"false\"\n   }\n}",
      "language": "json"
    },
    {
      "code": "<createShipmentResponse>\n   <result>\n      <hasErrors>false</hasErrors>\n      <hasOnlyRetryableErrors>false</hasOnlyRetryableErrors>\n      <hasWarnings>false</hasWarnings>\n      <shipmentNumber>0000005</shipmentNumber>\n      <carrierShipmentNumber>00000000000000</carrierShipmentNumber>\n      <packageResults>\n         <packageTransactionId>PACKAGE_TEST_1</packageTransactionId>\n         <referenceNumber1>PACKAGE_TEST_1</referenceNumber1>\n         <carrierPackageNumber>00000000000000</carrierPackageNumber>\n         <documents>\n            <documentType>DPD Label DE</documentType>\n            <mimeType>application/pdf</mimeType>\n            <content>...PDF Content base64 encoded...</content>\n         </documents>\n      </packageResults>\n      <accountInfo>\n         <customerNumberAtCarrier>1234567890</customerNumberAtCarrier>\n         <singlePackageHandlingActivated>false</singlePackageHandlingActivated>\n      </accountInfo>\n   </result>\n</createShipmentResponse>",
      "language": "xml",
      "name": ""
    }
  ]
}
[/block]
###Packed items
Some carriers or some shipping scenarios require that items are not just listed within the shipment, but they must be assigned to packages.
The following example shows how to pack items. You can combine it with the above example. 
[block:code]
{
  "codes": [
    {
      "code": "{\n   \"packageTypeIdentCode\":\"BOX\",\n   \"packageNumber\":\"1\",\n   \"packageTransactionId\":\"PACKAGE_TEST_1\",\n   \"referenceNumber1\":\"PACKAGE_TEST_1\",\n   \"grossWeight\":{\n      \"value\":\"25\",\n      \"unit\":\"kg\"\n   },\n   \"containedItems\":[\n      {\n         \"itemTransactionId\":\"ITEM_TEST_1\",\n         \"referenceNumber1\":\"ITEM_TEST_1\",\n         \"quantityValue\":\"10\"\n      }\n   ]\n}",
      "language": "json"
    },
    {
      "code": "<packages>\n   <packageTypeIdentCode>BOX</packageTypeIdentCode>\n   <packageNumber>1</packageNumber>\n   <packageTransactionId>PACKAGE_TEST_1</packageTransactionId>\n   <referenceNumber1>PACKAGE_TEST_1</referenceNumber1>\n   <grossWeight>\n      <value>25</value>\n      <unit>kg</unit>\n   </grossWeight>\n   <containedItems>\n      <itemTransactionId>ITEM_TEST_1</itemTransactionId>\n      <referenceNumber1>ITEM_TEST_1</referenceNumber1>\n      <quantityValue>10</quantityValue>\n   </containedItems>\n</packages>",
      "language": "xml"
    }
  ]
}
[/block]
##Shipping package by package
Many of our customers know very early in the shipping process where and with which carrier (and service) they want to ship. However, they may know only very late the details like the number of packages, exact weights, dimensions, etc. Once the package is ready, all necessary documents should be created and available as fast as possible. No problem :).
You simply need to create the shipping order with createShipment, add the packages with processShipment, and once you are done send another processShipment to complete the shipping order. If you know when adding the last package that it really is the last one, then you can complete the shipping order directly when adding the package.

###Creating the shipment
[block:code]
{
  "codes": [
    {
      "code": "{\n   \"clientSystemId\":\"SOAPUI\",\n   \"clientIdentCode\":\"APITEST\",\n   \"userName\":\"API_TEST\",\n   \"resultLanguageIsoCodes\":[\n      \"EN\"\n   ],\n   \"creationParms\":{\n      \"creationMode\":\"VALIDATION_OK\"\n   },\n   \"shipment\":{\n      \"transactionId\":\"SHIPMENT_TEST_1\",\n      \"transactionLabel\":\"SHIPMENT_TEST_1\",\n      \"isDocumentShipment\":\"false\",\n      \"referenceNumber1\":\"SHIPMENT_TEST_1\",\n      \"shippingDate\":\"2018-01-01\",\n      \"contents\":\"SHIPMENT_CONTENT\",\n      \"shippingPt\":{\n         \"companyNumber\":\"SHIP_COMPANY_1\",\n         \"name\":\"AEB Shipping Point\",\n         \"street\":\"AEB Street 1\",\n         \"postcode\":\"70567\",\n         \"city\":\"Stuttgart\",\n         \"countryISOCode\":\"DE\",\n         \"initFromCompanyMasterFileData\":\"false\"\n      },\n      \"shippingPtContact\":{\n         \"name\":\"Peter Maier\",\n         \"phone\":\"0049711728420\"\n      },\n      \"goodsValue\":{\n         \"value\":\"100\",\n         \"currencyIso\":\"EUR\"\n      },\n      \"consignee\":{\n         \"companyNumber\":\"CONSIGNEE_COMPANY_1\",\n         \"name\":\"Max Muster\",\n         \"street\":\"Muster Street 1\",\n         \"postcode\":\"3001\",\n         \"city\":\"Bern\",\n         \"countryISOCode\":\"CH\",\n         \"initFromCompanyMasterFileData\":\"false\"\n      },\n      \"consigneeContact\":{\n         \"name\":\"Max Muster\",\n         \"phone\":\"0049123456789\"\n      },\n      \"carrierIdentCode\":\"DPD_DE\",\n      \"serviceCode\":\"DPD_EXPR_INT\",\n      \"termsOfDeliveryCode\":\"DDP\"\n   },\n   \"processParms\":{\n      \"processMode\":{\n         \"mode\":\"EXTENDED\"\n      },\n      \"documentPrepareScope\":{\n         \"scope\":\"SHIPMENTONLY\"\n      },\n      \"workstationId\":\"PDF_WORKSTATION\",\n      \"documentOutputScope\":{\n         \"scope\":\"SHIPMENTONLY\"\n      },\n      \"documentOutputMode\":{\n         \"mode\":\"RETURN\"\n      },\n      \"doCompletion\":\"false\"\n   }\n}",
      "language": "json"
    },
    {
      "code": "<createShipment>\n   <request>\n      <clientSystemId>SOAPUI</clientSystemId>\n      <clientIdentCode>APITEST</clientIdentCode>\n      <userName>API_TEST</userName>\n      <resultLanguageIsoCodes>EN</resultLanguageIsoCodes>\n      <creationParms>\n         <creationMode>VALIDATION_OK</creationMode>\n      </creationParms>\n      <shipment>\n         <transactionId>SHIPMENT_TEST_1</transactionId>\n         <transactionLabel>SHIPMENT_TEST_1</transactionLabel>\n         <isDocumentShipment>false</isDocumentShipment>\n         <referenceNumber1>SHIPMENT_TEST_1</referenceNumber1>\n         <shippingDate>2018-01-01</shippingDate>\n         <contents>SHIPMENT_CONTENT</contents>\n         <shippingPt>\n            <companyNumber>SHIP_COMPANY_1</companyNumber>\n            <name>AEB Shipping Point</name>\n            <street>AEB Street 1</street>\n            <postcode>70567</postcode>\n            <city>Stuttgart</city>\n            <countryISOCode>DE</countryISOCode>\n            <initFromCompanyMasterFileData>false</initFromCompanyMasterFileData>\n         </shippingPt>\n         <shippingPtContact>\n            <name>Peter Maier</name>\n            <phone>0049711728420</phone>\n         </shippingPtContact>\n         <goodsValue>\n            <value>100</value>\n            <currencyIso>EUR</currencyIso>\n         </goodsValue>\n         <consignee>\n            <companyNumber>CONSIGNEE_COMPANY_1</companyNumber>\n            <name>Max Muster</name>\n            <street>Muster Street 1</street>\n            <postcode>3001</postcode>\n            <city>Bern</city>\n            <countryISOCode>CH</countryISOCode>\n            <initFromCompanyMasterFileData>false</initFromCompanyMasterFileData>\n         </consignee>\n         <consigneeContact>\n            <name>Max Muster</name>\n            <phone>0049123456789</phone>\n         </consigneeContact>\n         <carrierIdentCode>DPD_DE</carrierIdentCode>\n         <serviceCode>DPD_EXPR_INT</serviceCode>\n         <termsOfDeliveryCode>DDP</termsOfDeliveryCode>\n      </shipment>\n      <processParms>\n         <processMode>\n            <mode>EXTENDED</mode>\n         </processMode>\n         <documentPrepareScope>\n            <scope>SHIPMENTONLY</scope>\n         </documentPrepareScope>\n         <workstationId>PDF_WORKSTATION</workstationId>\n         <documentOutputScope>\n            <scope>SHIPMENTONLY</scope>\n         </documentOutputScope>\n         <documentOutputMode>\n            <mode>RETURN</mode>\n         </documentOutputMode>\n         <doCompletion>false</doCompletion>\n      </processParms>\n   </request>\n</createShipment>",
      "language": "xml"
    }
  ]
}
[/block]
**API Response to the above call**
[block:code]
{
  "codes": [
    {
      "code": "{\n   \"hasErrors\":\"false\",\n   \"hasOnlyRetryableErrors\":\"false\",\n   \"hasWarnings\":\"false\",\n   \"shipmentNumber\":\"0000011\",\n   \"accountInfo\":{\n      \"customerNumberAtCarrier\":\"1234567890\",\n      \"singlePackageHandlingActivated\":\"false\"\n   }\n}",
      "language": "json"
    },
    {
      "code": "<createShipmentResponse>\n   <result>\n      <hasErrors>false</hasErrors>\n      <hasOnlyRetryableErrors>false</hasOnlyRetryableErrors>\n      <hasWarnings>false</hasWarnings>\n      <shipmentNumber>0000011</shipmentNumber>\n      <accountInfo>\n         <customerNumberAtCarrier>1234567890</customerNumberAtCarrier>\n         <singlePackageHandlingActivated>false</singlePackageHandlingActivated>\n      </accountInfo>\n   </result>\n</createShipmentResponse>",
      "language": "xml"
    }
  ]
}
[/block]
###Adding the package
[block:code]
{
  "codes": [
    {
      "code": "{\n   \"clientSystemId\":\"SOAPUI\",\n   \"clientIdentCode\":\"APITEST\",\n   \"userName\":\"API_TEST\",\n   \"resultLanguageIsoCodes\":[\n      \"EN\"\n   ],\n   \"creationParms\":{\n      \"creationMode\":\"VALIDATION_OK\"\n   },\n   \"shipmentReference\":{\n      \"transactionId\":\"SHIPMENT_TEST_1\",\n      \"referenceNumber1\":\"SHIPMENT_TEST_1\"\n   },\n   \"packages\":[\n      {\n         \"packageTypeIdentCode\":\"BOX\",\n         \"packageNumber\":\"1\",\n         \"packageTransactionId\":\"PACKAGE_TEST_1\",\n         \"referenceNumber1\":\"PACKAGE_TEST_1\",\n         \"referenceNumber2\":\"PACKAGE_TEST_1\",\n         \"grossWeight\":{\n            \"value\":\"25\",\n            \"unit\":\"kg\"\n         }\n      }\n   ],\n   \"processParms\":{\n      \"processMode\":{\n         \"mode\":\"EXTENDED\"\n      },\n      \"documentPrepareScope\":{\n         \"scope\":\"REQUEST\"\n      },\n      \"workstationId\":\"PDF_WORKSTATION\",\n      \"documentOutputScope\":{\n         \"scope\":\"REQUEST\"\n      },\n      \"documentOutputMode\":{\n         \"mode\":\"RETURN\"\n      },\n      \"doCompletion\":\"false\"\n   }\n}",
      "language": "json"
    },
    {
      "code": "<processShipment>\n   <request>\n      <clientSystemId>SOAPUI</clientSystemId>\n      <clientIdentCode>APITEST</clientIdentCode>\n      <userName>API_TEST</userName>\n      <resultLanguageIsoCodes>EN</resultLanguageIsoCodes>\n      <creationParms>\n         <creationMode>VALIDATION_OK</creationMode>\n      </creationParms>\n      <shipmentReference>\n         <transactionId>SHIPMENT_TEST_1</transactionId>\n         <referenceNumber1>SHIPMENT_TEST_1</referenceNumber1>\n      </shipmentReference>\n      <packages>\n         <packageTypeIdentCode>BOX</packageTypeIdentCode>\n         <packageNumber>1</packageNumber>\n         <packageTransactionId>PACKAGE_TEST_1</packageTransactionId>\n         <referenceNumber1>PACKAGE_TEST_1</referenceNumber1>\n         <referenceNumber2>PACKAGE_TEST_1</referenceNumber2>\n         <grossWeight>\n            <value>25</value>\n            <unit>kg</unit>\n         </grossWeight>\n      </packages>\n      <processParms>\n         <processMode>\n            <mode>EXTENDED</mode>\n         </processMode>\n         <documentPrepareScope>\n            <scope>REQUEST</scope>\n         </documentPrepareScope>\n         <workstationId>PDF_WORKSTATION</workstationId>\n         <documentOutputScope>\n            <scope>REQUEST</scope>\n         </documentOutputScope>\n         <documentOutputMode>\n            <mode>RETURN</mode>\n         </documentOutputMode>\n         <doCompletion>false</doCompletion>\n      </processParms>\n   </request>\n</processShipment>",
      "language": "xml"
    }
  ]
}
[/block]
**API Response to the above call**
[block:code]
{
  "codes": [
    {
      "code": "{\n   \"hasErrors\":\"false\",\n   \"hasOnlyRetryableErrors\":\"false\",\n   \"hasWarnings\":\"false\",\n   \"carrierShipmentNumber\":\"00000000000000\",\n   \"packageResults\":{\n      \"packageTransactionId\":\"PACKAGE_TEST_1\",\n      \"referenceNumber1\":\"PACKAGE_TEST_1\",\n      \"carrierPackageNumber\":\"00000000000000\",\n      \"documents\":{\n         \"documentType\":\"DPD Label DE\",\n         \"mimeType\":\"application/pdf\",\n         \"content\":\"PDF Content in Base64 encoded\"\n      }\n   }\n}",
      "language": "json"
    },
    {
      "code": "<processShipmentResponse>\n   <result>\n      <hasErrors>false</hasErrors>\n      <hasOnlyRetryableErrors>false</hasOnlyRetryableErrors>\n      <hasWarnings>false</hasWarnings>\n      <carrierShipmentNumber>00000000000000</carrierShipmentNumber>\n      <packageResults>\n         <packageTransactionId>PACKAGE_TEST_1</packageTransactionId>\n         <referenceNumber1>PACKAGE_TEST_1</referenceNumber1>\n         <carrierPackageNumber>00000000000000</carrierPackageNumber>\n         <documents>\n            <documentType>DPD Label DE</documentType>\n            <mimeType>application/pdf</mimeType>\n            <content>PDF Content in Base64 encoded</content>\n         </documents>\n      </packageResults>\n   </result>\n</processShipmentResponse>",
      "language": "xml"
    }
  ]
}
[/block]
###Completing the shipment
[block:code]
{
  "codes": [
    {
      "code": "{\n   \"clientSystemId\":\"SOAPUI\",\n   \"clientIdentCode\":\"APITEST\",\n   \"userName\":\"API_TEST\",\n   \"resultLanguageIsoCodes\":[\n      \"EN\"\n   ],\n   \"creationParms\":{\n      \"creationMode\":\"VALIDATION_OK\"\n   },\n   \"shipmentReference\":{\n      \"transactionId\":\"SHIPMENT_TEST_1\",\n      \"referenceNumber1\":\"SHIPMENT_TEST_1\"\n   },\n   \"processParms\":{\n      \"processMode\":{\n         \"mode\":\"EXTENDED\"\n      },\n      \"documentPrepareScope\":{\n         \"scope\":\"REMAINING\"\n      },\n      \"workstationId\":\"PDF_WORKSTATION\",\n      \"documentOutputScope\":{\n         \"scope\":\"REMAINING\"\n      },\n      \"documentOutputMode\":{\n         \"mode\":\"RETURN\"\n      },\n      \"doCompletion\":\"true\"\n   }\n}",
      "language": "json"
    },
    {
      "code": "<processShipment>\n   <request>\n      <clientSystemId>SOAPUI</clientSystemId>\n      <clientIdentCode>APITEST</clientIdentCode>\n      <userName>API_TEST</userName>\n      <resultLanguageIsoCodes>EN</resultLanguageIsoCodes>\n      <creationParms>\n         <creationMode>VALIDATION_OK</creationMode>\n      </creationParms>\n      <shipmentReference>\n         <transactionId>SHIPMENT_TEST_1</transactionId>\n         <referenceNumber1>SHIPMENT_TEST_1</referenceNumber1>\n      </shipmentReference>\n      <processParms>\n         <processMode>\n            <mode>EXTENDED</mode>\n         </processMode>\n         <documentPrepareScope>\n            <scope>REMAINING</scope>\n         </documentPrepareScope>\n         <workstationId>PDF_WORKSTATION</workstationId>\n         <documentOutputScope>\n            <scope>REMAINING</scope>\n         </documentOutputScope>\n         <documentOutputMode>\n            <mode>RETURN</mode>\n         </documentOutputMode>\n         <doCompletion>true</doCompletion>\n      </processParms>\n   </request>\n</processShipment>",
      "language": "xml"
    }
  ]
}
[/block]
**API Response to the above call**
[block:code]
{
  "codes": [
    {
      "code": "{\n   \"hasErrors\":\"false\",\n   \"hasOnlyRetryableErrors\":\"false\",\n   \"hasWarnings\":\"false\",\n   \"carrierShipmentNumber\":\"00000000000000\",\n   \"packageResults\":{\n      \"packageTransactionId\":\"PACKAGE_TEST_1\",\n      \"referenceNumber1\":\"PACKAGE_TEST_1\",\n      \"carrierPackageNumber\":\"00000000000000\"\n   }\n}",
      "language": "json"
    },
    {
      "code": "<processShipmentResponse>\n   <result>\n      <hasErrors>false</hasErrors>\n      <hasOnlyRetryableErrors>false</hasOnlyRetryableErrors>\n      <hasWarnings>false</hasWarnings>\n      <carrierShipmentNumber>00000000000000</carrierShipmentNumber>\n      <packageResults>\n         <packageTransactionId>PACKAGE_TEST_1</packageTransactionId>\n         <referenceNumber1>PACKAGE_TEST_1</referenceNumber1>\n         <carrierPackageNumber>00000000000000</carrierPackageNumber>\n      </packageResults>\n   </result>\n</processShipmentResponse>",
      "language": "xml"
    }
  ]
}
[/block]
##Adding (more) items
You need to add another delivery note to an already existing shipment? This is also done by *processShipment*. 
Note: Sometimes it is necessary to update the shipment. In this example, adding items usually increases the value of the shipment. We are very conservative towards updates. However, the fields available for updates are located in the *shipmentUpdateData* structure.
The example shows you how it works:
[block:code]
{
  "codes": [
    {
      "code": "{\n   \"clientSystemId\":\"SOAPUI\",\n   \"clientIdentCode\":\"APITEST\",\n   \"userName\":\"API_TEST\",\n   \"resultLanguageIsoCodes\":[\n      \"EN\"\n   ],\n   \"creationParms\":{\n      \"creationMode\":\"VALIDATION_OK\"\n   },\n   \"shipmentReference\":{\n      \"transactionId\":\"SHIPMENT_TEST_1\",\n      \"referenceNumber1\":\"SHIPMENT_TEST_1\"\n   },\n   \"shipmentTotals\":{\n      \"numberOfPackagesExpected\":\"3\",\n      \"grossWeightExpected\":{\n         \"value\":\"10\",\n         \"unit\":\"kg\"\n      },\n      \"loadingMeters\":\"10\",\n      \"palletPlaces\":\"1\"\n   },\n   \"shipmentUpdateData\":{\n      \"shippingDate\":\"2018-01-01\",\n      \"customsValue\":{\n         \"value\":\"100\",\n         \"currencyIso\":\"EUR\"\n      },\n      \"goodsValue\":{\n         \"value\":\"100\",\n         \"currencyIso\":\"EUR\"\n      }\n   },\n   \"items\":[\n      {\n         \"itemNumber\":\"1\",\n         \"itemTransactionId\":\"ITEM_TEST_1\",\n         \"referenceNumber1\":\"ITEM_TEST_1\",\n         \"description\":\"Pancake\",\n         \"countryOfOriginsISOCode\":\"DE\",\n         \"certificateOfOrigins\":\"DE\",\n         \"quantity\":{\n            \"value\":\"10\",\n            \"unit\":\"kg\"\n         },\n         \"customsValue\":{\n            \"value\":\"100\",\n            \"currencyIso\":\"EUR\"\n         },\n         \"goodsValue\":{\n            \"value\":\"100\",\n            \"currencyIso\":\"EUR\"\n         }\n      }\n   ],\n   \"processParms\":{\n      \"processMode\":{\n         \"mode\":\"EXTENDED\"\n      },\n      \"documentPrepareScope\":{\n         \"scope\":\"REMAINING\"\n      },\n      \"workstationId\":\"PDF_WORKSTATION\",\n      \"documentOutputScope\":{\n         \"scope\":\"REMAINING\"\n      },\n      \"documentOutputMode\":{\n         \"mode\":\"RETURN\"\n      },\n      \"doCompletion\":\"true\"\n   }\n}",
      "language": "json"
    },
    {
      "code": "<processShipment>\n   <request>\n      <clientSystemId>SOAPUI</clientSystemId>\n      <clientIdentCode>APITEST</clientIdentCode>\n      <userName>API_TEST</userName>\n      <resultLanguageIsoCodes>EN</resultLanguageIsoCodes>\n      <creationParms>\n         <creationMode>VALIDATION_OK</creationMode>\n      </creationParms>\n      <shipmentReference>\n         <transactionId>SHIPMENT_TEST_1</transactionId>\n         <referenceNumber1>SHIPMENT_TEST_1</referenceNumber1>\n      </shipmentReference>\n      <shipmentTotals>\n         <numberOfPackagesExpected>3</numberOfPackagesExpected>\n         <grossWeightExpected>\n            <value>10</value>\n            <unit>kg</unit>\n         </grossWeightExpected>\n         <loadingMeters>10</loadingMeters>\n         <palletPlaces>1</palletPlaces>\n      </shipmentTotals>\n      <shipmentUpdateData>\n         <shippingDate>2018-01-01</shippingDate>\n         <customsValue>\n            <value>100</value>\n            <currencyIso>EUR</currencyIso>\n         </customsValue>\n         <goodsValue>\n            <value>100</value>\n            <currencyIso>EUR</currencyIso>\n         </goodsValue>\n      </shipmentUpdateData>\n      <items>\n         <itemNumber>1</itemNumber>\n         <itemTransactionId>ITEM_TEST_1</itemTransactionId>\n         <referenceNumber1>ITEM_TEST_1</referenceNumber1>\n         <description>Pancake</description>\n         <countryOfOriginsISOCode>DE</countryOfOriginsISOCode>\n         <certificateOfOrigins>DE</certificateOfOrigins>\n         <quantity>\n            <value>10</value>\n            <unit>kg</unit>\n         </quantity>\n         <customsValue>\n            <value>100</value>\n            <currencyIso>EUR</currencyIso>\n         </customsValue>\n         <goodsValue>\n            <value>100</value>\n            <currencyIso>EUR</currencyIso>\n         </goodsValue>\n      </items>\n      <processParms>\n         <processMode>\n            <mode>EXTENDED</mode>\n         </processMode>\n         <documentPrepareScope>\n            <scope>REMAINING</scope>\n         </documentPrepareScope>\n         <workstationId>PDF_WORKSTATION</workstationId>\n         <documentOutputScope>\n            <scope>REMAINING</scope>\n         </documentOutputScope>\n         <documentOutputMode>\n            <mode>RETURN</mode>\n         </documentOutputMode>\n         <doCompletion>true</doCompletion>\n      </processParms>\n   </request>\n</processShipment>",
      "language": "xml"
    }
  ]
}
[/block]
**API Response to the above call**
[block:code]
{
  "codes": [
    {
      "code": "{\n   \"hasErrors\":\"false\",\n   \"hasOnlyRetryableErrors\":\"false\",\n   \"hasWarnings\":\"false\",\n   \"carrierShipmentNumber\":\"00000000000000\",\n   \"packageResults\":{\n      \"packageTransactionId\":\"PACKAGE_TEST_1\",\n      \"referenceNumber1\":\"PACKAGE_TEST_1\",\n      \"carrierPackageNumber\":\"00000000000000\"\n   }\n}",
      "language": "json"
    },
    {
      "code": "<processShipmentResponse>\n   <result>\n      <hasErrors>false</hasErrors>\n      <hasOnlyRetryableErrors>false</hasOnlyRetryableErrors>\n      <hasWarnings>false</hasWarnings>\n      <carrierShipmentNumber>00000000000000</carrierShipmentNumber>\n      <packageResults>\n         <packageTransactionId>PACKAGE_TEST_1</packageTransactionId>\n         <referenceNumber1>PACKAGE_TEST_1</referenceNumber1>\n         <carrierPackageNumber>00000000000000</carrierPackageNumber>\n      </packageResults>\n   </result>\n</processShipmentResponse>",
      "language": "xml"
    }
  ]
}
[/block]