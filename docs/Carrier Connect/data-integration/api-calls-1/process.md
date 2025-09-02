---
title: Update
excerpt: >-
  Learn how to use the Carrier Connect API calls to programmatically UPDATE
  existing shipments or pickups.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
<HTMLBlock>{`
<style>
  span.cm-s-neo {
    background-color: #f2f2f2;
    color: red;
  }
</style>
`}</HTMLBlock>

# processShipment: Update a shipping order

The <a href="https://transport-freight-management.docs.developers.aeb.com/reference/processshipment" target="_blank">processShipment</a> call allows you to make updates to an existing <Glossary>shipping order</Glossary>. 

This includes adding packages or performing various operations, such as updating the shipping date or customs value. Moreover, you can easily trigger document (label) preparation and document output as needed.

## Adding a package

A package is described within the `packages` section. It has its own references and attributes.

```json
{
  ...
  "packages": {
    "packageTypeIdentCode": "?",
    "packageSpecificeContents": "?",
    "packageNumber": "?",
    "packageTransactionId": "?",
    "referenceNumber1": "?",
    "referenceNumber2": "?",
    "grossWeight": {
      "value": "?",
      "unit": "?"
    },
    "dimensions": {
      "length": "?",
      "width": "?",
      "height": "?",
      "identCode": "?"
    }
  }
}
```
```xml
...
<packages>
         <packageTypeIdentCode>?</packageTypeIdentCode>
         <packageSpecificeContents>?</packageSpecificeContents>
         <packageNumber>?</packageNumber>
         <packageTransactionId>?</packageTransactionId>
         <referenceNumber1>?</referenceNumber1>
         <referenceNumber2>?</referenceNumber2>
         <grossWeight>
              <value>?</value>
              <unit>?</unit>
          </grossWeight>
          <dimensions>
              <length>?</length>
              <width>?</width>
              <height>?</height>
              <identCode>?</identCode>
           </dimensions>
              ...
</packages>
```

## Adding items

Items can be added using either <a href="https://transport-freight-management.docs.developers.aeb.com/reference/createshipment" target="_blank">createShipment</a> or <a href="https://transport-freight-management.docs.developers.aeb.com/reference/processshipment" target="_blank">processShipment</a>.\
Of course, a combination of both is also possible. Here's an example:

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

And the response:

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

When adding items using *processShipment*, it could be necessary to <a href="https://carrierconnect.docs.developers.aeb.com/docs/update-shipment-data-1" target="_blank">update</a> some other shipment values e.g. customs value or goods value.

## Updating shipment data

With a *processShipment* call you can update specific fields of an existing shipment. You can update:

* **Shipment totals** (`shipmentTotals`) like number of packages, weights of the shipment, or total number of pallet places
* **Specific fields** (`shipmentUpdateData`) such as shipping date or values concerning insurance and goods

```json
{
  "shipmentTotals": {
    "numberOfPackagesExpected": "?",
    "grossWeightExpected": {
      "value": "?",
      "unit": "?"
    },
    "loadingMeters": "?",
    "palletPlaces": "?"
  },
  "shipmentUpdateData": {
    "shippingDate": "?",
    "codValue": {
      "value": "?",
      "currencyIso": "?"
    },
    "insuranceValue": {
      "value": "?",
      "currencyIso": "?"
    },
    "goodsValue": {
      "value": "?",
      "currencyIso": "?"
    },
    "customsValue": {
      "value": "?",
      "currencyIso": "?"
    },
    "customsRegistrationNumber": "?",
    "remark": "?"
  }
}
```
```xml
<shipmentTotals>
	<numberOfPackagesExpected>?</numberOfPackagesExpected>
	<grossWeightExpected>
		<value>?</value>
		<unit>?</unit>
	</grossWeightExpected>
	<loadingMeters>?</loadingMeters>
	<palletPlaces>?</palletPlaces>
</shipmentTotals>
<shipmentUpdateData>
	<shippingDate>?</shippingDate>
	<codValue>
		<value>?</value>
		<currencyIso>?</currencyIso>
	</codValue>
	<insuranceValue>
		<value>?</value>
		<currencyIso>?</currencyIso>
	</insuranceValue>
	<goodsValue>
		<value>?</value>
		<currencyIso>?</currencyIso>
	</goodsValue>
	<customsValue>
		<value>?</value>
		<currencyIso>?</currencyIso>
	</customsValue>
	<customsRegistrationNumber>?</customsRegistrationNumber>
	<remark>?</remark>
</shipmentUpdateData>
```

## Completing the shipment

<CompletingTheShipment />

# updateCustomsData: Update customs data

Updates customs data for an existing shipment. Updates data on shipment and item level. Updates customs relevant data only.

API Reference: <a href="https://transport-freight-management.docs.developers.aeb.com/reference/updatecustomsdata" target="_blank">update</a>

# processPickup: Update a pickup

By utilizing the <a href="https://transport-freight-management.docs.developers.aeb.com/reference/processpickup" target="_blank">processPickup</a> call, you can seamlessly add new shipping orders to an existing pickup that has not yet been closed. 

Additionally, this API call allows you to print or reprint manifest documents for a pickup. 

<Callout icon="💡" theme="default">
  ### This functionality proves beneficial, especially in scenarios, where manifest documents were not printed during the "createPickup" call or when a reprint of these documents becomes necessary.
</Callout>
