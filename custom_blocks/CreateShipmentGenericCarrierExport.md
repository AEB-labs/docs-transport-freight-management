---
name: createShipment (Generic Carrier, Export)
---
```json
{
  "clientSystemId": "Carrier Connect Client Name",
  "clientIdentCode": "Host System Name",
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
		"transactionId": "516513218",
		"referenceNumber1": "1000000",
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
			"city": "Zürich",
			"companyNumber": "3000",
			"countryISOCode": "CH",
			"name": "AEB Schweiz AG",
			"postcode": "8005",
			"street": "Sihlquai 131"
		},
		"consigneeContact": {
			"name": "AEB Empfang Schweiz",
			"phone": "+41 43 211 1060"
		},
		"customsValue": {
			"currencyIso": "EUR",
			"value": 1050
		},
		"goodsValue": {
			"currencyIso": "EUR",
			"value": 1000
		},
		"items": [
			{
				"itemTransactionId": "100015681351",
				"referenceNumber1": "1000-1",
				"description": "Item #1 description",
				"countryOfOriginsISOCode": "DE",
				"customsTariffNumber": 82054000,
				"customsValue": {
					"currencyIso": "EUR",
					"value": 105
				},
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
				"packageTransactionId": "77702165",
				"packageTypeIdentCode": "CT",
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
		],
		"referencesTexts": [
			{
				"type": "CUSTOMS_REGISTRATION_NUMBER",
				"value": "MRN123456789"
			},
			{
				"type": "INVOICE_NUMBER",
				"value": "INV123456789"
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
    <transactionId>516513218</transactionId>
    <referenceNumber1>1000000</referenceNumber1>
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
      <city>Zürich</city>
      <companyNumber>3000</companyNumber>
      <countryISOCode>CH</countryISOCode>
      <name>AEB Schweiz AG</name>
      <postcode>8005</postcode>
      <street>Sihlquai 131</street>
    </consignee>
    <consigneeContact>
      <name>AEB Empfang Schweiz</name>
      <phone>+41 43 211 1060</phone>
    </consigneeContact>
    <customsValue>
      <currencyIso>EUR</currencyIso>
      <value>1050</value>
    </customsValue>
    <goodsValue>
      <currencyIso>EUR</currencyIso>
      <value>1000</value>
    </goodsValue>
    <items>
      <itemTransactionId>100015681351</itemTransactionId>
      <referenceNumber1>1000-1</referenceNumber1>
      <description>Item #1 description</description>
      <countryOfOriginsISOCode>DE</countryOfOriginsISOCode>
      <customsTariffNumber>82054000</customsTariffNumber>
      <customsValue>
        <currencyIso>EUR</currencyIso>
        <value>105</value>
      </customsValue>
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
      <packageTransactionId>77702165</packageTransactionId>
      <packageTypeIdentCode>CT</packageTypeIdentCode>
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
    <referencesTexts>
      <referenceText>
        <type>CUSTOMS_REGISTRATION_NUMBER</type>
        <value>MRN123456789</value>
      </referenceText>
      <referenceText>
        <type>INVOICE_NUMBER</type>
        <value>INV123456789</value>
      </referenceText>
    </referencesTexts>
  </shipment>
```
