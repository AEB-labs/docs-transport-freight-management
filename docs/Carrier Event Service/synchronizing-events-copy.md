---
title: Synchronizing events
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
[block:html]
{
  "html": "<style>\n  span.cm-s-neo {\n    background-color: #f2f2f2;\n    color: red;\n  }\n</style>"
}
[/block]


It is possible to import resolved carrier tracking events into your host system. For this purpose you can use the [synchronizeResolvedEvents](https://transport-freight-management.docs.developers.aeb.com/reference/synchronizeresolvedevents) API call.

For the **first request** you should use the `ageInDays` parameter which returns all carrier events later than the value of `ageInDays`. 

In the API response you will also get back a `syncId` which can be used in all **subsequent requests** instead of the `ageInDays` parameter. For more information regarding the `syncId` have a look [here](https://transport-freight-management.docs.developers.aeb.com/docs/sync#using-syncid).

The following is an example for a `synchronizeResolvedEvents` request:

```xml
<request>
	<clientSystemId>TEST_ID</clientSystemId>
	<clientIdentCode>APITEST</clientIdentCode>
	<userName>API_TEST</userName>
	<resultLanguageIsoCodes>en</resultLanguageIsoCodes>
	<resultLanguageIsoCodes>de</resultLanguageIsoCodes>
	<syncId></syncId>
	<ageInDays>5</ageInDays>
	<blockSize>200</blockSize>
	<isStandardEventTextIncluded>true</isStandardEventTextIncluded>
	<isOriginalDescriptionIncluded>true</isOriginalDescriptionIncluded>
</request>
```
```json
{
     "clientSystemId": "TEST_ID",
     "clientIdentCode": "APITEST",
     "userName": "API_TEST",
     "resultLanguageIsoCodes": [
          "en",
          "de"
     ],
     "ageInDays": 5,
     "blockSize": 200,
     "isStandardEventTextIncluded": true,
     "isOriginalDescriptionIncluded": true
}
```

- **Endpoints**:  
  `https://xnsg.dc.aeb.com/{{cco_system}}/rest/CarrierEventServiceBFBean/synchronizeResolvedEvents`.  
  Replace `{{cco_system}}` with the actuall CES engine: 
  - `prod1ces` if you're using Carrier Connect `prod1cai`
  - `prod2ces` if you're using `prod2cai`.
- The `blockSize` default is 200. In the API response the field `isComplete` indicates, if there are more than 200 events - in this case it is false, otherwise it’s true. So you should check that field and if it is false immediately send another request until `isComplete = true`.
- For the authentication credentials and for the field value of `clientSystemId` please contact AEB.

> ❗️ An event can only be synchronized 30 days after the event occurred.

# AEB Standard Events

You can find an explanation of the AEB standard events [here](https://rz3.aeb.de/docudata/data-sheets/cross-product/datasheet-aebengines-standardevents/en-US/index.html#684553611684580491).

# FAQ

| Question                                                  | Answer                                                                                                                                                                                                          |
| :-------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| How often does CES collect event data from the carriers?  | Usually every 5 minutes (in exceptional cases up to 15). That depends on the carrier. AEB endeavors to collect data as often as possible, we align ourselves with the specifications of the respective carrier. |
| How to handle events where trackingObjectType = SHIPMENT? | In this case no package level tracking is possible in principle. However, the corresponding event can be used for every package of the shipment                                                                 |