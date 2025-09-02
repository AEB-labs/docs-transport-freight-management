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

> 📘 Keeping data and documents right
>
> **Due to the various shipping scenarios our customers are faced with, Carrier Connect provides maximum flexibility in its API.** However, this means that you have to keep in mind that after you've started printing documents all following changes might alter the data printed on the documents. It is your responsibility to make sure that no negative consequences on your processes and the carriers' operational processes result from these subsequent changes.

## Shipping with only one API call

In some cases, processes allow that all shipping data are available and finalized. No changes are expected anymore.\
This provides an easy context and makes it possible to ship by just sending one API call. With this one call you can create the shipment, include packages and items, complete the shipment, and request that documents should be returned in the response.

**An example with one package:**

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
      "isDocumentShipment":"false",
      "referenceNumber1":"SHIPMENT_TEST_1",
      "shippingDate":"2018-01-01",
      "contents":"SHIPMENT_CONTENT",
      "shippingPt":{
         "companyNumber":"SHIP_COMPANY_1",
         "name":"AEB Shipping Point",
         "street":"AEB Street 1",
         "postcode":"70567",
         "city":"Stuttgart",
         "countryISOCode":"DE",
         "initFromCompanyMasterFileData":"false"
      },
      "shippingPtContact":{
         "name":"Peter Maier",
         "phone":"0049711728420"
      },
      "consignee":{
         "companyNumber":"CONSIGNEE_COMPANY_1",
         "name":"Max Muster",
         "street":"Muster Street 1",
         "postcode":"10555",
         "city":"Berlin",
         "countryISOCode":"DE",
         "initFromCompanyMasterFileData":"false"
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
         <isDocumentShipment>false</isDocumentShipment>
         <referenceNumber1>SHIPMENT_TEST_1</referenceNumber1>
         <shippingDate>2018-01-01</shippingDate>
         <contents>SHIPMENT_CONTENT</contents>
         <shippingPt>
            <companyNumber>SHIP_COMPANY_1</companyNumber>
            <name>AEB Shipping Point</name>
            <street>AEB Street 1</street>
            <postcode>70567</postcode>
            <city>Stuttgart</city>
            <countryISOCode>DE</countryISOCode>
            <initFromCompanyMasterFileData>false</initFromCompanyMasterFileData>
         </shippingPt>
         <shippingPtContact>
            <name>Peter Maier</name>
            <phone>0049711728420</phone>
         </shippingPtContact>
         <consignee>
            <companyNumber>CONSIGNEE_COMPANY_1</companyNumber>
            <name>Max Muster</name>
            <street>Muster Street 1</street>
            <postcode>10555</postcode>
            <city>Berlin</city>
            <countryISOCode>DE</countryISOCode>
            <initFromCompanyMasterFileData>false</initFromCompanyMasterFileData>
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

**API Response to the above call**

```json
{
   "hasErrors":"false",
   "hasOnlyRetryableErrors":"false",
   "hasWarnings":"false",
   "shipmentNumber":"0000005",
   "carrierShipmentNumber":"00000000000000",
   "packageResults":{
      "packageTransactionId":"PACKAGE_TEST_1",
      "referenceNumber1":"PACKAGE_TEST_1",
      "carrierPackageNumber":"00000000000000",
      "documents":{
         "documentType":"DPD Label DE",
         "mimeType":"application/pdf",
         "content":"PDF Content in Base64 encoded"
      }
   },
   "accountInfo":{
      "customerNumberAtCarrier":"1234567890",
      "singlePackageHandlingActivated":"false"
   }
}
```
```xml
<createShipmentResponse>
   <result>
      <hasErrors>false</hasErrors>
      <hasOnlyRetryableErrors>false</hasOnlyRetryableErrors>
      <hasWarnings>false</hasWarnings>
      <shipmentNumber>0000005</shipmentNumber>
      <carrierShipmentNumber>00000000000000</carrierShipmentNumber>
      <packageResults>
         <packageTransactionId>PACKAGE_TEST_1</packageTransactionId>
         <referenceNumber1>PACKAGE_TEST_1</referenceNumber1>
         <carrierPackageNumber>00000000000000</carrierPackageNumber>
         <documents>
            <documentType>DPD Label DE</documentType>
            <mimeType>application/pdf</mimeType>
            <content>...PDF Content base64 encoded...</content>
         </documents>
      </packageResults>
      <accountInfo>
         <customerNumberAtCarrier>1234567890</customerNumberAtCarrier>
         <singlePackageHandlingActivated>false</singlePackageHandlingActivated>
      </accountInfo>
   </result>
</createShipmentResponse>
```

### Packed items

Some carriers or some shipping scenarios require that items are not just listed within the shipment, but they must be assigned to packages.\
The following example shows how to pack items. You can combine it with the above example. 

```json
{
   "packageTypeIdentCode":"BOX",
   "packageNumber":"1",
   "packageTransactionId":"PACKAGE_TEST_1",
   "referenceNumber1":"PACKAGE_TEST_1",
   "grossWeight":{
      "value":"25",
      "unit":"kg"
   },
   "containedItems":[
      {
         "itemTransactionId":"ITEM_TEST_1",
         "referenceNumber1":"ITEM_TEST_1",
         "quantityValue":"10"
      }
   ]
}
```
```xml
<packages>
   <packageTypeIdentCode>BOX</packageTypeIdentCode>
   <packageNumber>1</packageNumber>
   <packageTransactionId>PACKAGE_TEST_1</packageTransactionId>
   <referenceNumber1>PACKAGE_TEST_1</referenceNumber1>
   <grossWeight>
      <value>25</value>
      <unit>kg</unit>
   </grossWeight>
   <containedItems>
      <itemTransactionId>ITEM_TEST_1</itemTransactionId>
      <referenceNumber1>ITEM_TEST_1</referenceNumber1>
      <quantityValue>10</quantityValue>
   </containedItems>
</packages>
```

## Shipping package by package

Many of our customers know very early in the shipping process where and with which carrier (and service) they want to ship. However, they may know only very late the details like the number of packages, exact weights, dimensions, etc. Once the package is ready, all necessary documents should be created and available as fast as possible. No problem :).\
You simply need to create the shipping order with createShipment, add the packages with processShipment, and once you are done send another processShipment to complete the shipping order. If you know when adding the last package that it really is the last one, then you can complete the shipping order directly when adding the package.

### Creating the shipment

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
      "isDocumentShipment":"false",
      "referenceNumber1":"SHIPMENT_TEST_1",
      "shippingDate":"2018-01-01",
      "contents":"SHIPMENT_CONTENT",
      "shippingPt":{
         "companyNumber":"SHIP_COMPANY_1",
         "name":"AEB Shipping Point",
         "street":"AEB Street 1",
         "postcode":"70567",
         "city":"Stuttgart",
         "countryISOCode":"DE",
         "initFromCompanyMasterFileData":"false"
      },
      "shippingPtContact":{
         "name":"Peter Maier",
         "phone":"0049711728420"
      },
      "goodsValue":{
         "value":"100",
         "currencyIso":"EUR"
      },
      "consignee":{
         "companyNumber":"CONSIGNEE_COMPANY_1",
         "name":"Max Muster",
         "street":"Muster Street 1",
         "postcode":"3001",
         "city":"Bern",
         "countryISOCode":"CH",
         "initFromCompanyMasterFileData":"false"
      },
      "consigneeContact":{
         "name":"Max Muster",
         "phone":"0049123456789"
      },
      "carrierIdentCode":"DPD_DE",
      "serviceCode":"DPD_EXPR_INT",
      "termsOfDeliveryCode":"DDP"
   },
   "processParms":{
      "processMode":{
         "mode":"EXTENDED"
      },
      "documentPrepareScope":{
         "scope":"SHIPMENTONLY"
      },
      "workstationId":"PDF_WORKSTATION",
      "documentOutputScope":{
         "scope":"SHIPMENTONLY"
      },
      "documentOutputMode":{
         "mode":"RETURN"
      },
      "doCompletion":"false"
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
         <isDocumentShipment>false</isDocumentShipment>
         <referenceNumber1>SHIPMENT_TEST_1</referenceNumber1>
         <shippingDate>2018-01-01</shippingDate>
         <contents>SHIPMENT_CONTENT</contents>
         <shippingPt>
            <companyNumber>SHIP_COMPANY_1</companyNumber>
            <name>AEB Shipping Point</name>
            <street>AEB Street 1</street>
            <postcode>70567</postcode>
            <city>Stuttgart</city>
            <countryISOCode>DE</countryISOCode>
            <initFromCompanyMasterFileData>false</initFromCompanyMasterFileData>
         </shippingPt>
         <shippingPtContact>
            <name>Peter Maier</name>
            <phone>0049711728420</phone>
         </shippingPtContact>
         <goodsValue>
            <value>100</value>
            <currencyIso>EUR</currencyIso>
         </goodsValue>
         <consignee>
            <companyNumber>CONSIGNEE_COMPANY_1</companyNumber>
            <name>Max Muster</name>
            <street>Muster Street 1</street>
            <postcode>3001</postcode>
            <city>Bern</city>
            <countryISOCode>CH</countryISOCode>
            <initFromCompanyMasterFileData>false</initFromCompanyMasterFileData>
         </consignee>
         <consigneeContact>
            <name>Max Muster</name>
            <phone>0049123456789</phone>
         </consigneeContact>
         <carrierIdentCode>DPD_DE</carrierIdentCode>
         <serviceCode>DPD_EXPR_INT</serviceCode>
         <termsOfDeliveryCode>DDP</termsOfDeliveryCode>
      </shipment>
      <processParms>
         <processMode>
            <mode>EXTENDED</mode>
         </processMode>
         <documentPrepareScope>
            <scope>SHIPMENTONLY</scope>
         </documentPrepareScope>
         <workstationId>PDF_WORKSTATION</workstationId>
         <documentOutputScope>
            <scope>SHIPMENTONLY</scope>
         </documentOutputScope>
         <documentOutputMode>
            <mode>RETURN</mode>
         </documentOutputMode>
         <doCompletion>false</doCompletion>
      </processParms>
   </request>
</createShipment>
```

**API Response to the above call**

```json
{
   "hasErrors":"false",
   "hasOnlyRetryableErrors":"false",
   "hasWarnings":"false",
   "shipmentNumber":"0000011",
   "accountInfo":{
      "customerNumberAtCarrier":"1234567890",
      "singlePackageHandlingActivated":"false"
   }
}
```
```xml
<createShipmentResponse>
   <result>
      <hasErrors>false</hasErrors>
      <hasOnlyRetryableErrors>false</hasOnlyRetryableErrors>
      <hasWarnings>false</hasWarnings>
      <shipmentNumber>0000011</shipmentNumber>
      <accountInfo>
         <customerNumberAtCarrier>1234567890</customerNumberAtCarrier>
         <singlePackageHandlingActivated>false</singlePackageHandlingActivated>
      </accountInfo>
   </result>
</createShipmentResponse>
```

### Adding the package

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
   "shipmentReference":{
      "transactionId":"SHIPMENT_TEST_1",
      "referenceNumber1":"SHIPMENT_TEST_1"
   },
   "packages":[
      {
         "packageTypeIdentCode":"BOX",
         "packageNumber":"1",
         "packageTransactionId":"PACKAGE_TEST_1",
         "referenceNumber1":"PACKAGE_TEST_1",
         "referenceNumber2":"PACKAGE_TEST_1",
         "grossWeight":{
            "value":"25",
            "unit":"kg"
         }
      }
   ],
   "processParms":{
      "processMode":{
         "mode":"EXTENDED"
      },
      "documentPrepareScope":{
         "scope":"REQUEST"
      },
      "workstationId":"PDF_WORKSTATION",
      "documentOutputScope":{
         "scope":"REQUEST"
      },
      "documentOutputMode":{
         "mode":"RETURN"
      },
      "doCompletion":"false"
   }
}
```
```xml
<processShipment>
   <request>
      <clientSystemId>SOAPUI</clientSystemId>
      <clientIdentCode>APITEST</clientIdentCode>
      <userName>API_TEST</userName>
      <resultLanguageIsoCodes>EN</resultLanguageIsoCodes>
      <creationParms>
         <creationMode>VALIDATION_OK</creationMode>
      </creationParms>
      <shipmentReference>
         <transactionId>SHIPMENT_TEST_1</transactionId>
         <referenceNumber1>SHIPMENT_TEST_1</referenceNumber1>
      </shipmentReference>
      <packages>
         <packageTypeIdentCode>BOX</packageTypeIdentCode>
         <packageNumber>1</packageNumber>
         <packageTransactionId>PACKAGE_TEST_1</packageTransactionId>
         <referenceNumber1>PACKAGE_TEST_1</referenceNumber1>
         <referenceNumber2>PACKAGE_TEST_1</referenceNumber2>
         <grossWeight>
            <value>25</value>
            <unit>kg</unit>
         </grossWeight>
      </packages>
      <processParms>
         <processMode>
            <mode>EXTENDED</mode>
         </processMode>
         <documentPrepareScope>
            <scope>REQUEST</scope>
         </documentPrepareScope>
         <workstationId>PDF_WORKSTATION</workstationId>
         <documentOutputScope>
            <scope>REQUEST</scope>
         </documentOutputScope>
         <documentOutputMode>
            <mode>RETURN</mode>
         </documentOutputMode>
         <doCompletion>false</doCompletion>
      </processParms>
   </request>
</processShipment>
```

**API Response to the above call**

```json
{
   "hasErrors":"false",
   "hasOnlyRetryableErrors":"false",
   "hasWarnings":"false",
   "carrierShipmentNumber":"00000000000000",
   "packageResults":{
      "packageTransactionId":"PACKAGE_TEST_1",
      "referenceNumber1":"PACKAGE_TEST_1",
      "carrierPackageNumber":"00000000000000",
      "documents":{
         "documentType":"DPD Label DE",
         "mimeType":"application/pdf",
         "content":"PDF Content in Base64 encoded"
      }
   }
}
```
```xml
<processShipmentResponse>
   <result>
      <hasErrors>false</hasErrors>
      <hasOnlyRetryableErrors>false</hasOnlyRetryableErrors>
      <hasWarnings>false</hasWarnings>
      <carrierShipmentNumber>00000000000000</carrierShipmentNumber>
      <packageResults>
         <packageTransactionId>PACKAGE_TEST_1</packageTransactionId>
         <referenceNumber1>PACKAGE_TEST_1</referenceNumber1>
         <carrierPackageNumber>00000000000000</carrierPackageNumber>
         <documents>
            <documentType>DPD Label DE</documentType>
            <mimeType>application/pdf</mimeType>
            <content>PDF Content in Base64 encoded</content>
         </documents>
      </packageResults>
   </result>
</processShipmentResponse>
```

### Completing the shipment

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
   "shipmentReference":{
      "transactionId":"SHIPMENT_TEST_1",
      "referenceNumber1":"SHIPMENT_TEST_1"
   },
   "processParms":{
      "processMode":{
         "mode":"EXTENDED"
      },
      "documentPrepareScope":{
         "scope":"REMAINING"
      },
      "workstationId":"PDF_WORKSTATION",
      "documentOutputScope":{
         "scope":"REMAINING"
      },
      "documentOutputMode":{
         "mode":"RETURN"
      },
      "doCompletion":"true"
   }
}
```
```xml
<processShipment>
   <request>
      <clientSystemId>SOAPUI</clientSystemId>
      <clientIdentCode>APITEST</clientIdentCode>
      <userName>API_TEST</userName>
      <resultLanguageIsoCodes>EN</resultLanguageIsoCodes>
      <creationParms>
         <creationMode>VALIDATION_OK</creationMode>
      </creationParms>
      <shipmentReference>
         <transactionId>SHIPMENT_TEST_1</transactionId>
         <referenceNumber1>SHIPMENT_TEST_1</referenceNumber1>
      </shipmentReference>
      <processParms>
         <processMode>
            <mode>EXTENDED</mode>
         </processMode>
         <documentPrepareScope>
            <scope>REMAINING</scope>
         </documentPrepareScope>
         <workstationId>PDF_WORKSTATION</workstationId>
         <documentOutputScope>
            <scope>REMAINING</scope>
         </documentOutputScope>
         <documentOutputMode>
            <mode>RETURN</mode>
         </documentOutputMode>
         <doCompletion>true</doCompletion>
      </processParms>
   </request>
</processShipment>
```

**API Response to the above call**

```json
{
   "hasErrors":"false",
   "hasOnlyRetryableErrors":"false",
   "hasWarnings":"false",
   "carrierShipmentNumber":"00000000000000",
   "packageResults":{
      "packageTransactionId":"PACKAGE_TEST_1",
      "referenceNumber1":"PACKAGE_TEST_1",
      "carrierPackageNumber":"00000000000000"
   }
}
```
```xml
<processShipmentResponse>
   <result>
      <hasErrors>false</hasErrors>
      <hasOnlyRetryableErrors>false</hasOnlyRetryableErrors>
      <hasWarnings>false</hasWarnings>
      <carrierShipmentNumber>00000000000000</carrierShipmentNumber>
      <packageResults>
         <packageTransactionId>PACKAGE_TEST_1</packageTransactionId>
         <referenceNumber1>PACKAGE_TEST_1</referenceNumber1>
         <carrierPackageNumber>00000000000000</carrierPackageNumber>
      </packageResults>
   </result>
</processShipmentResponse>
```

## Adding (more) items

You need to add another delivery note to an already existing shipment? This is also done by *processShipment*.\
Note: Sometimes it is necessary to update the shipment. In this example, adding items usually increases the value of the shipment. We are very conservative towards updates. However, the fields available for updates are located in the *shipmentUpdateData* structure.\
The example shows you how it works:

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
   "shipmentReference":{
      "transactionId":"SHIPMENT_TEST_1",
      "referenceNumber1":"SHIPMENT_TEST_1"
   },
   "shipmentTotals":{
      "numberOfPackagesExpected":"3",
      "grossWeightExpected":{
         "value":"10",
         "unit":"kg"
      },
      "loadingMeters":"10",
      "palletPlaces":"1"
   },
   "shipmentUpdateData":{
      "shippingDate":"2018-01-01",
      "customsValue":{
         "value":"100",
         "currencyIso":"EUR"
      },
      "goodsValue":{
         "value":"100",
         "currencyIso":"EUR"
      }
   },
   "items":[
      {
         "itemNumber":"1",
         "itemTransactionId":"ITEM_TEST_1",
         "referenceNumber1":"ITEM_TEST_1",
         "description":"Pancake",
         "countryOfOriginsISOCode":"DE",
         "certificateOfOrigins":"DE",
         "quantity":{
            "value":"10",
            "unit":"kg"
         },
         "customsValue":{
            "value":"100",
            "currencyIso":"EUR"
         },
         "goodsValue":{
            "value":"100",
            "currencyIso":"EUR"
         }
      }
   ],
   "processParms":{
      "processMode":{
         "mode":"EXTENDED"
      },
      "documentPrepareScope":{
         "scope":"REMAINING"
      },
      "workstationId":"PDF_WORKSTATION",
      "documentOutputScope":{
         "scope":"REMAINING"
      },
      "documentOutputMode":{
         "mode":"RETURN"
      },
      "doCompletion":"true"
   }
}
```
```xml
<processShipment>
   <request>
      <clientSystemId>SOAPUI</clientSystemId>
      <clientIdentCode>APITEST</clientIdentCode>
      <userName>API_TEST</userName>
      <resultLanguageIsoCodes>EN</resultLanguageIsoCodes>
      <creationParms>
         <creationMode>VALIDATION_OK</creationMode>
      </creationParms>
      <shipmentReference>
         <transactionId>SHIPMENT_TEST_1</transactionId>
         <referenceNumber1>SHIPMENT_TEST_1</referenceNumber1>
      </shipmentReference>
      <shipmentTotals>
         <numberOfPackagesExpected>3</numberOfPackagesExpected>
         <grossWeightExpected>
            <value>10</value>
            <unit>kg</unit>
         </grossWeightExpected>
         <loadingMeters>10</loadingMeters>
         <palletPlaces>1</palletPlaces>
      </shipmentTotals>
      <shipmentUpdateData>
         <shippingDate>2018-01-01</shippingDate>
         <customsValue>
            <value>100</value>
            <currencyIso>EUR</currencyIso>
         </customsValue>
         <goodsValue>
            <value>100</value>
            <currencyIso>EUR</currencyIso>
         </goodsValue>
      </shipmentUpdateData>
      <items>
         <itemNumber>1</itemNumber>
         <itemTransactionId>ITEM_TEST_1</itemTransactionId>
         <referenceNumber1>ITEM_TEST_1</referenceNumber1>
         <description>Pancake</description>
         <countryOfOriginsISOCode>DE</countryOfOriginsISOCode>
         <certificateOfOrigins>DE</certificateOfOrigins>
         <quantity>
            <value>10</value>
            <unit>kg</unit>
         </quantity>
         <customsValue>
            <value>100</value>
            <currencyIso>EUR</currencyIso>
         </customsValue>
         <goodsValue>
            <value>100</value>
            <currencyIso>EUR</currencyIso>
         </goodsValue>
      </items>
      <processParms>
         <processMode>
            <mode>EXTENDED</mode>
         </processMode>
         <documentPrepareScope>
            <scope>REMAINING</scope>
         </documentPrepareScope>
         <workstationId>PDF_WORKSTATION</workstationId>
         <documentOutputScope>
            <scope>REMAINING</scope>
         </documentOutputScope>
         <documentOutputMode>
            <mode>RETURN</mode>
         </documentOutputMode>
         <doCompletion>true</doCompletion>
      </processParms>
   </request>
</processShipment>
```

**API Response to the above call**

```json
{
   "hasErrors":"false",
   "hasOnlyRetryableErrors":"false",
   "hasWarnings":"false",
   "carrierShipmentNumber":"00000000000000",
   "packageResults":{
      "packageTransactionId":"PACKAGE_TEST_1",
      "referenceNumber1":"PACKAGE_TEST_1",
      "carrierPackageNumber":"00000000000000"
   }
}
```
```xml
<processShipmentResponse>
   <result>
      <hasErrors>false</hasErrors>
      <hasOnlyRetryableErrors>false</hasOnlyRetryableErrors>
      <hasWarnings>false</hasWarnings>
      <carrierShipmentNumber>00000000000000</carrierShipmentNumber>
      <packageResults>
         <packageTransactionId>PACKAGE_TEST_1</packageTransactionId>
         <referenceNumber1>PACKAGE_TEST_1</referenceNumber1>
         <carrierPackageNumber>00000000000000</carrierPackageNumber>
      </packageResults>
   </result>
</processShipmentResponse>
```
