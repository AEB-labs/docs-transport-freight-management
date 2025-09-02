---
title: Common Shipping Scenarios
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
There are two main options how to integrate the shipping order and label creation into your shipping process. This decision is crucial for which API calls you are implementing. 

**Option 1 - Simple shipping:**

- You can create data for all physical packages first and then print all labels at once at the end of the packing process. 

**Option 2 - Advanced Shipping:**

- Or you can print labels one by one per package, i.e. as soon as the first package is physically created, a label can be be printed, then second package, second label etc. The shipment will be left open for further package processing during the day. Finally, with the last package or a separate API call the shipment needs to be closed.

> 📘 
> 
> Prerequisite is single-package handling being activated in the account setup of the carrier configuration. You configure the so-called single package handling under _Carrier configurations – Accounts – Single pkg. handling_ field group: enable option. If this option cannot be activated, it is not supported by the interface of the carrier.

# Simple shipping: Printing labels at once at the end of the packing process

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/119de37559edc026c88aeb59e1b581d59dd754aecce18d42eeee84aa99921a07-Get_Started_Carrier_Connect_JWA_-_Collective_Package_Handling.jpg",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


**Use case**

In some cases, processes allow that all shipping data is available and finalized. No changes are expected anymore.  
This provides an easy context and makes it possible to ship by just sending one API call. With this one call you can create the shipment, include packages and items, complete the shipment, and request documents to be returned in the response.

**Consequences**

- The overall number of packages is already known when you start printing labels. It is possible to print total values on the labels, e.g. "1 of 5", "2 of 5" as package counter or even total weight of the shipment.
- This is often preferred by the carriers, especially LTL carriers. 

## Overview of the necessary API calls

1. _[createShipment](https://transport-freight-management.docs.developers.aeb.com/reference/createshipment)_: create shipment containing all packages, request all label documents, parameter `doCompletion` = `true`

## Example API call

Here's an example, where we create a shipment with one package. `documentPrepareScope` and `documentOutputScope` are set to `ALL` (for more information see [🔧 Process Parameters](doc:processparms)), so we are requesting all shipment documents. `doCompletion`is set to `true`, which means the shipment data can't be changed anymore and it's ready to be assigned to a pickup:

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

And this is how the response looks like:

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

# Printing labels one by one per package

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/dc748a63c388e436683e130de7709663653ec156d5ee3f1cc71f9e7eb3b177fd-Get_Started_Carrier_Connect_JWA_-_Single_Package_Handling.jpg",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


**Use case**

Many of our customers know very early in the shipping process where and with which carrier (and service) they want to ship. However, they may know only very late the details like the total number of packages, exact total weights, dimensions, etc. Once each of the packages is ready, it is processed and the label should be printed. The shipment remains open until the very last minute for further packages to be added.  
You simply need to create the shipping order with _createShipment_, add the packages with _processShipment_, and once you are done send another _processShipment_ to complete the shipping order. You can also complete the shipping order with the last package, i.e. with the last processShipment call.

**Consequences **

- Allows you to add packages one by one to the shipping order. Therefore, you can delete packages or repack them easier, without cancelling the whole shipping order. 
- You get labels right away (no need to buffer or risk of having unlabeled packages)
- You will not be able to print total values on the labels, e.g. "1 of 5", "2 of 5", except you know the total package number or total weight of the shipment already with the first package. 

## Overview of the necessary API calls

1. [_createShipment_](https://transport-freight-management.docs.developers.aeb.com/reference/createshipment): create shipment without packages or with only the first package
2. n times: [_processShipment_](https://transport-freight-management.docs.developers.aeb.com/reference/processshipment): add a package, request label documents. For detailed information see [🔄 Update](doc:process).
3. When shipment status in ERP is closed, then _processShipment_ with paremeter `doCompletion` = `true`

## Example API call

Here's a createShipment example, where we're just creating the shipment without any packages. 

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

Consequently we don't get back any documents in the response:

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