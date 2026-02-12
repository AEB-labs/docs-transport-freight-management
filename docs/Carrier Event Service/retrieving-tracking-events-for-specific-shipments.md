---
title: Retrieving tracking events for specific shipments
deprecated: false
hidden: true
metadata:
  robots: index
---
If you want to retrieve tracking events for specific shipments on demand, you can use the `getShipmentsEvents` method.

This method returns the complete tracking information currently available in Carrier Event Service (CES) for the provided shipment references. 

### Request

You must provide the technical client context as well as at least one shipment reference.

The request contains:

* `clientSystemId`
* `clientIdentCode`
* `userName`
* `shipmentReferences` – list of shipments to retrieve
* Optional language and text flags:
  * `resultLanguageIsoCodes`
  * `isStandardEventTextIncluded`
  * `isOriginalDescriptionIncluded`

Each entry in `shipmentReferences` identifies a shipment, for example by:

* `shipmentNumber`
* `transactionId`
* `clientSystemId`
* `organizationUnitClientSystem`

<br />

The following is an example for a `getShipmentsEvents` request:

```json
{
  "clientSystemId": "TEST_ID",
  "clientIdentCode": "APITEST",
  "userName": "API_TEST",
  "resultLanguageIsoCodes": [
    "en",
    "de"
  ],
  "shipmentReferences": [
    {
      "shipmentNumber": "0181374",
      "transactionId": "WA1-100696235133571361984584754FZOD-2110",
      "clientSystemId": "PS4_100",
      "organizationUnitClientSystem": "AL_US"
    }
  ],
  "isStandardEventTextIncluded": true,
  "isOriginalDescriptionIncluded": true
}
```
```xml
<?xml version="1.0" encoding="UTF-8"?>
<getShipmentsEventsRequestDTO>
	<clientSystemId>TEST_ID</clientSystemId>
	<clientIdentCode>APITEST</clientIdentCode>
	<userName>API_TEST</userName>
	<resultLanguageIsoCodes>en</resultLanguageIsoCodes>
	<resultLanguageIsoCodes>de</resultLanguageIsoCodes>
	<shipmentReferences>
		<shipmentNumber>0181374</shipmentNumber>
		<transactionId>WA1-100696235133571361984584754FZOD-2110</transactionId>
		<clientSystemId>PS4_100</clientSystemId>
		<organizationUnitClientSystem>AL_US</organizationUnitClientSystem>
	</shipmentReferences>
	<isStandardEventTextIncluded>true</isStandardEventTextIncluded>
	<isOriginalDescriptionIncluded>true</isOriginalDescriptionIncluded>
</getShipmentsEventsRequestDTO>

```

<br />

<br />

## Response

The response contains a general processing status and a list of shipments.

Each entry in `shipments` represents one requested shipment and contains:

* `hasErrors`
* `hasWarnings`
* `messages`
* `shipmentReference`
* Optional `referenceNumber1`
* `trackingObjects`

Each `trackingObject` contains:

* `trackingNumber`
* `trackingObjectType`
* `isReturnTrackingObject`
* Optional `trackingStart`
* Optional `trackingFinish`
* `trackingEvents`

Each `trackingEvent` includes:

* `identCode` (standardized event code)
* `originalIdentCode`
* `originalReason`
* `eventDate` (including timezone)
* Optional `originalLocation`
* Optional `additionalData`
* `eventText`
  * `standardEventText` (if requested)
  * `originalDescription` (if requested)

Example response:

```json
{
  "hasErrors": false,
  "hasOnlyRetryableErrors": true,
  "hasWarnings": true,
  "messages": [
    {
      "messageType": "WARNING",
      "messageIdentCode": "5627",
      "messageTexts": [
        {
          "languageISOCode": "en",
          "text": "Some free-form text"
        }
      ],
      "indentationLevel": 0
    }
  ],
  "shipments": [
    {
      "hasErrors": true,
      "hasWarnings": true,
      "messages": [
        {
          "messageType": "WARNING",
          "messageIdentCode": "5627",
          "messageTexts": [
            {
              "languageISOCode": "en",
              "text": "Some free-form text"
            }
          ],
          "indentationLevel": 0
        }
      ],
      "shipmentReference": {
        "shipmentNumber": "0181374",
        "transactionId": "WA1-100696235133571361984584754FZOD-2110",
        "clientSystemId": "PS4_100",
        "organizationUnitClientSystem": "AL_US"
      },
      "referenceNumber1": "704503458358845172150809",
      "trackingObjects": [
        {
          "trackingNumber": "AB486 083 50",
          "isReturnTrackingObject": true,
          "trackingObjectType": "SHIPMENT",
          "trackingStart": {
            "dateInTimezone": "string",
            "timezone": "string"
          },
          "trackingFinish": {
            "dateInTimezone": "string",
            "timezone": "string"
          },
          "trackingEvents": [
            {
              "identCode": "IOD",
              "originalIdentCode": "L420",
              "originalReason": "BZ",
              "eventDate": {
                "dateInTimezone": "string",
                "timezone": "string"
              },
              "originalLocation": {
                "address": {
                  "street": "Sigmaringer Str. 109",
                  "postcode": "70567",
                  "city": "Stuttgart",
                  "countryISOCode": "DE",
                  "stateRegion": "Baden-Württemberg"
                },
                "geoCoordinates": {
                  "latitude": -6.2649875,
                  "longitude": 106.8766384
                },
                "identifier": {
                  "type": "UNLOCODE",
                  "value": "KRSEL"
                },
                "description": "Some description of the location used by the carrier"
              },
              "additionalData": [
                {
                  "additionalDataType": "CARRIER_NOTE",
                  "value": "Some carrier note"
                }
              ],
              "eventText": {
                "standardEventText": [
                  {
                    "languageISOCode": "en",
                    "name": "Delivered",
                    "description": "The shipment was delivered"
                  }
                ],
                "originalDescription": "Some original description from the carrier"
              }
            }
          ]
        }
      ]
    }
  ]
}
```
```xml
<?xml version="1.0" encoding="UTF-8"?>
<getShipmentsEventsResponseDTO>
	<hasErrors>false</hasErrors>
	<hasOnlyRetryableErrors>true</hasOnlyRetryableErrors>
	<hasWarnings>true</hasWarnings>
	<messages>
		<messageType>WARNING</messageType>
		<messageIdentCode>5627</messageIdentCode>
		<messageTexts>
			<languageISOCode>en</languageISOCode>
			<text>Some free-form text</text>
		</messageTexts>
		<indentationLevel>0</indentationLevel>
	</messages>
	<shipments>
		<hasErrors>true</hasErrors>
		<hasWarnings>true</hasWarnings>
		<messages>
			<messageType>WARNING</messageType>
			<messageIdentCode>5627</messageIdentCode>
			<messageTexts>
				<languageISOCode>en</languageISOCode>
				<text>Some free-form text</text>
			</messageTexts>
			<indentationLevel>0</indentationLevel>
		</messages>
		<shipmentReference>
			<shipmentNumber>0181374</shipmentNumber>
			<transactionId>WA1-100696235133571361984584754FZOD-2110</transactionId>
			<clientSystemId>PS4_100</clientSystemId>
			<organizationUnitClientSystem>AL_US</organizationUnitClientSystem>
		</shipmentReference>
		<referenceNumber1>704503458358845172150809</referenceNumber1>
		<trackingObjects>
			<trackingNumber>AB486 083 50</trackingNumber>
			<isReturnTrackingObject>true</isReturnTrackingObject>
			<trackingObjectType>SHIPMENT</trackingObjectType>
			<trackingStart>
				<dateInTimezone>string</dateInTimezone>
				<timezone>string</timezone>
			</trackingStart>
			<trackingFinish>
				<dateInTimezone>string</dateInTimezone>
				<timezone>string</timezone>
			</trackingFinish>
			<trackingEvents>
				<identCode>IOD</identCode>
				<originalIdentCode>L420</originalIdentCode>
				<originalReason>BZ</originalReason>
				<eventDate>
					<dateInTimezone>string</dateInTimezone>
					<timezone>string</timezone>
				</eventDate>
				<originalLocation>
					<address>
						<street>Sigmaringer Str. 109</street>
						<postcode>70567</postcode>
						<city>Stuttgart</city>
						<countryISOCode>DE</countryISOCode>
						<stateRegion>Baden-Württemberg</stateRegion>
					</address>
					<geoCoordinates>
						<latitude>-6.2649875</latitude>
						<longitude>106.8766384</longitude>
					</geoCoordinates>
					<identifier>
						<type>UNLOCODE</type>
						<value>KRSEL</value>
					</identifier>
					<description>Some description of the location used by the carrier</description>
				</originalLocation>
				<additionalData>
					<additionalDataType>CARRIER_NOTE</additionalDataType>
					<value>Some carrier note</value>
				</additionalData>
				<eventText>
					<standardEventText>
						<languageISOCode>en</languageISOCode>
						<name>Delivered</name>
						<description>The shipment was delivered</description>
					</standardEventText>
					<originalDescription>Some original description from the carrier</originalDescription>
				</eventText>
			</trackingEvents>
		</trackingObjects>
	</shipments>
</getShipmentsEventsResponseDTO>
```
