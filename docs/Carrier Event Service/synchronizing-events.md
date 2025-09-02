---
title: Synchronizing events
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
A possibility for requesting all resolved carrier events that have occurred since the last synchronization call is given with [synchronizeResolvedEvents](https://transport-freight-management.docs.developers.aeb.com/reference/synchronizeresolvedevents). A carrier event is resolved if it is assigned to a tracking object. 
[block:callout]
{
  "type": "danger",
  "body": "Please note that the Carrier Event Service is an additional product and the API refers to another URL. \n\nBefore you can start using the Carrier Event Service API, you need a user and a password. If you do not have your own client yet, you can use the following credentials to test the API:\n\nClient: APITEST\nUser: API_TEST\nPassword: API_TEST2018\n\nThe client APITEST is intended for basic connectivity testing and is used by different users. Don't use it with sensitive data."
}
[/block]
To use this synchronization call, a partner system subscription has to be defined. Since the partner system subscription provides that the carrier events are available for the synchronization call, only carrier events received after the partner system subscription is enabled can be synchronized. The installation ID of the partner system subscription is used in the synchronization call with the field ‘clientSystemId’.

For the request, a sync ID or a parameter named 'ageInDays' have to be filled in to get the corresponding carrier events. The parameter ‘ageInDays’ is typically used to initialize delta transmissions, so the call returns all carrier events later than ‘ageInDays’. After the initialization call, the sync ID is used instead of ‘ageInDays’.

The call returns all events that have occurred since the last synchronization call or more specifically since the provided sync ID. The response also contains a sync ID to use in subsequent calls. 

The following is an example for the synchronizeResolvedEvents request:
[block:code]
{
  "codes": [
    {
      "code": "<request>\n\t<clientSystemId>TEST_ID</clientSystemId>\n\t<clientIdentCode>APITEST</clientIdentCode>\n\t<userName>API_TEST</userName>\n\t<resultLanguageIsoCodes>en</resultLanguageIsoCodes>\n\t<resultLanguageIsoCodes>de</resultLanguageIsoCodes>\n\t<syncId></syncId>\n\t<ageInDays>5</ageInDays>\n\t<blockSize>200</blockSize>\n\t<isStandardEventTextIncluded>true</isStandardEventTextIncluded>\n\t<isOriginalDescriptionIncluded>true</isOriginalDescriptionIncluded>\n</request>\n",
      "language": "xml"
    }
  ]
}
[/block]