---
title: Synchronizing events (ALT)
excerpt: ''
deprecated: true
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
A possibility for requesting all resolved carrier events that have occurred since the last synchronization call is given with [synchronizeResolvedEvents](https://transport-freight-management.docs.developers.aeb.com/reference/synchronizeresolvedevents). A carrier event is resolved if it is assigned to a tracking object. 

> ❗️
>
> Please note that the Carrier Event Service is an additional product and the API refers to another URL. 
>
> Before you can start using the Carrier Event Service API, you need a user and a password. If you do not have your own client yet, you can use the following credentials to test the API:
>
> Client: APITEST\
> User: API\_TEST\
> Password: API\_TEST2018
>
> The client APITEST is intended for basic connectivity testing and is used by different users. Don't use it with sensitive data.

To use this synchronization call, a partner system subscription has to be defined. Since the partner system subscription provides that the carrier events are available for the synchronization call, only carrier events received after the partner system subscription is enabled can be synchronized. The installation ID of the partner system subscription is used in the synchronization call with the field ‘clientSystemId’.

For the request, a sync ID or a parameter named 'ageInDays' have to be filled in to get the corresponding carrier events. The parameter ‘ageInDays’ is typically used to initialize delta transmissions, so the call returns all carrier events later than ‘ageInDays’. After the initialization call, the sync ID is used instead of ‘ageInDays’.

The call returns all events that have occurred since the last synchronization call or more specifically since the provided sync ID. The response also contains a sync ID to use in subsequent calls. 

The following is an example for the synchronizeResolvedEvents request:

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
