---
name: createShipment (Generic Carrier, Domestic)
---
```json
{
	"clientSystemId": "Host System Name",
	"clientIdentCode": "Carrier Connect Client Name",
	"userName": "User Name",
	"resultLanguageIsoCodes": [
		"de"
	],
	"creationParms": {
		"creationMode": "VALIDATION_OK"
	},
	"processParms": {
		"processMode": {
			"mode": "EXTENDED"
		},
		"documentPrepareScope": {
			"scope": "ALL"
		},
		"workstationId": "ZPL203_A4LASER",
		"documentOutputScope": {
			"scope": "ALL"
		},
		"documentOutputMode": {
			"mode": "RETURN"
		},
		"doCompletion": true
	},
	"shipment": {
		"transactionId": "516513219",
		"referenceNumber1": "1000001",
		"carrierIdentCode": "GENERICCARRIER",
		"serviceCode": "STD",
		"termsOfDeliveryCode": "EXW",
		"contents": "spare parts",
		"shippingDate": "2025-01-10",
		"shippingPt": {
			"city": "Stuttgart",
			"companyNumber": "1000",
			"countryISOCode": "DE",
			"name": "AEB SE",
			"postcode": "70567",
			"street": "Sigmaringer Straße 109"
		},
		"shippingPtContact": {
			"name": "AEB Support",
			"phone": "+49 711 72842 110"
		},
		"consignee": {
			"city": "München",
			"companyNumber": "2000",
			"countryISOCode": "DE",
			"name": "AEB München",
			"postcode": "81249",
			"street": "Franz-Josef-Delonge-Strasse 7"
		},
		"consigneeContact": {
			"name": "AEB Empfang München",
			"phone": "0891490267-0"
		},
		"goodsValue": {
			"currencyIso": "EUR",
			"value": 1000
		},
		"items": [
			{
				"itemTransactionId": "100015681352",
				"referenceNumber1": "1000-1",
				"description": "Item #1 description",
				"goodsValue": {
					"currencyIso": "EUR",
					"value": 100
				},
				"grossWeight": {
					"unit": "kg",
					"value": 6
				},
				"quantity": {
					"unit": "St",
					"value": 10
				}
			}
		],
		"packages": [
			{
				"packageTransactionId": "77702167",
				"packageTypeIdentCode": "PAL",
				"grossWeight": {
					"unit": "kg",
					"value": 6.25
				},
				"dimensions": {
					"length": 10,
					"width": 10,
					"height": 10,
					"identCode": "cm"
				}
			}
		]
	}
}
```
```xml
<clientSystemId>Carrier Connect Client Name</clientSystemId>
<clientIdentCode>Host System Name</clientIdentCode>
<userName>User Name</userName>
<resultLanguageIsoCodes>de</resultLanguageIsoCodes>
<creationParms>
	<creationMode>VALIDATION_OK</creationMode>
</creationParms>
<processParms>
	<processMode>
		<mode>EXTENDED</mode>
	</processMode>
	<documentPrepareScope>
		<scope>ALL</scope>
	</documentPrepareScope>
	<workstationId>ZPL203_A4LASER</workstationId>
	<documentOutputScope>
		<scope>ALL</scope>
	</documentOutputScope>
	<documentOutputMode>
		<mode>RETURN</mode>
	</documentOutputMode>
	<doCompletion>true</doCompletion>
</processParms>
<shipment>
	<transactionId>516513219</transactionId>
	<referenceNumber1>1000001</referenceNumber1>
	<carrierIdentCode>GENERICCARRIER</carrierIdentCode>
	<serviceCode>STD</serviceCode>
	<termsOfDeliveryCode>EXW</termsOfDeliveryCode>
	<contents>spare parts</contents>
	<shippingDate>2025-01-10</shippingDate>
	<shippingPt>
		<city>Stuttgart</city>
		<companyNumber>1000</companyNumber>
		<countryISOCode>DE</countryISOCode>
		<name>AEB SE</name>
		<postcode>70567</postcode>
		<street>Sigmaringer Straße 109</street>
	</shippingPt>
	<shippingPtContact>
		<name>AEB Support</name>
		<phone>+49 711 72842 110</phone>
	</shippingPtContact>
	<consignee>
		<city>München</city>
		<companyNumber>2000</companyNumber>
		<countryISOCode>DE</countryISOCode>
		<name>AEB München</name>
		<postcode>81249</postcode>
		<street>Franz-Josef-Delonge-Strasse 7</street>
	</consignee>
	<consigneeContact>
		<name>AEB Empfang München</name>
		<phone>0891490267-0</phone>
	</consigneeContact>
	<goodsValue>
		<currencyIso>EUR</currencyIso>
		<value>1000</value>
	</goodsValue>
	<items>
    <itemTransactionId>100015681352</itemTransactionId>
    <referenceNumber1>1000-1</referenceNumber1>
    <description>Item #1 description</description>
    <goodsValue>
      <currencyIso>EUR</currencyIso>
      <value>100</value>
    </goodsValue>
    <grossWeight>
      <unit>kg</unit>
      <value>6</value>
    </grossWeight>
    <quantity>
      <unit>St</unit>
      <value>10</value>
    </quantity>
	</items>
	<packages>
    <packageTransactionId>77702167</packageTransactionId>
    <packageTypeIdentCode>PAL</packageTypeIdentCode>
    <grossWeight>
      <unit>kg</unit>
      <value>6.25</value>
    </grossWeight>
    <dimensions>
      <length>10</length>
      <width>10</width>
      <height>10</height>
      <identCode>cm</identCode>
    </dimensions>
	</packages>
</shipment>

```
