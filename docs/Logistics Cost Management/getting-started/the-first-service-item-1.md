---
title: The first service item
excerpt: Prepared calls for copy/paste in your development environment
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
In case you already use your own client: Before you start with your first service item in your own client, make sure that your Logistics Cost Management client is set up with a valid contract and a valid assigned price scheme.

To allow you to start quickly, you will find here a complete call to create a service item and receive a typical response.

## Creating a service item

You can use the example and copy/paste it into your favorite tool to test SOAP and/or REST API calls (The XML example below refers to SOAP. For REST XML please see: [https://rz3.aeb.de/demo1billing/swagger/](https://rz3.aeb.de/demo1billing/swagger/)). Our test environment is prepared to work with the data in this example.\
The additional data ("extendedData") used in this example is for the freight use case and uses the standard freight data. A detailed description of the standard freight data can be found [here](doc:freight-data).

```json
{
	"clientSystemId": "APITEST",
	"clientIdentCode": "APITEST",
	"userName": "user",
	"resultLanguageIsoCodes": [
		"de",
		"en"
	],
	"parms": {
		"calculatePriceImmediately": "false",
		"createSettlementsImmediately": "false",
		"returnTraceInfo": "true"
	},
	"items": [
		{
			"itemId": "25-11-2022",
			"scenarioIdentCode": "A01",
			"serviceIdentCode": "TNTDE_EXP12",
			"referenceNumber": "25-11-2022",
			"orderNumber": "25-11-2022",
			"serviceProvider": {
				"companyNumber": "TNT",
				"name": "TNT Express Worldwide",
				"street": "Heilbronner Staße 110",
				"postcode": "70334",
				"city": "Stuttgart",
				"countryISOCode": "DE"
			},
			"orderer": {
				"companyNumber": "001",
				"name": "AEB SE",
				"street": "Sigmaringer Straße 109",
				"postcode": "70567",
				"city": "Stuttgart",
				"countryISOCode": "DE"
			},
			"payer": {
				"companyNumber": "001",
				"name": "AEB SE",
				"street": "Sigmaringer Straße 109",
				"postcode": "70567",
				"city": "Stuttgart",
				"countryISOCode": "DE"
			},
			"beneficiary": {
				"companyNumber": "001",
				"name": "AEB SE",
				"street": "Sigmaringer Straße 109",
				"postcode": "70567",
				"city": "Stuttgart",
				"countryISOCode": "DE"
			},
			"referenceDate": {
				"dateInTimezone": "2022-11-25 12:00:00",
				"timezone": "Europe/Berlin"
			},
			"pricingDate": {
				"dateInTimezone": "2022-11-25 12:00:00",
				"timezone": "Europe/Berlin"
			},
			"chargeDate": {
				"dateInTimezone": "2022-11-25 12:00:00",
				"timezone": "Europe/Berlin"
			},
			"serviceDate": {
				"dateInTimezone": "2022-11-25 12:00:00",
				"timezone": "Europe/Berlin"
			},
			"orderDate": {
				"dateInTimezone": "2022-11-25 12:00:00",
				"timezone": "Europe/Berlin"
			},
			"quantity": {
				"value": "1",
				"unit": "St"
			},
			"description": "Shipment",
			"extendedData": {
				"fields": [
					{
						"name": "carrierDefinitionIdentCode",
						"type": "string",
						"value": "TNT"
					},
					{
						"name": "numberOfInvoices",
						"type": "decimal",
						"value": "1"
					},
					{
						"name": "isDangerousGoods",
						"type": "boolean",
						"value": "false"
					},
					{
						"name": "referenceNumber",
						"type": "string",
						"value": "referenceNumber"
					},
					{
						"name": "incotermIdentCode",
						"type": "string",
						"value": "incoterm"
					},
					{
						"name": "numberOfItems",
						"type": "decimal",
						"value": "2"
					},
					{
						"name": "palletPlaces",
						"type": "decimal",
						"value": "1.000"
					},
					{
						"name": "numberOfPackages",
						"type": "decimal",
						"value": "2"
					},
					{
						"name": "isDocumentShipment",
						"type": "boolean",
						"value": "false"
					},
					{
						"name": "numberOfDeliveryNotes",
						"type": "decimal",
						"value": "1"
					}
				],
				"subrecords": [
					{
						"name": "volume",
						"record": {
							"fields": [
								{
									"name": "unit",
									"type": "string",
									"value": "ccm"
								},
								{
									"name": "value",
									"type": "decimal",
									"value": "4500.000"
								}
							]
						}
					},
					{
						"name": "grossWeight",
						"record": {
							"fields": [
								{
									"name": "unit",
									"type": "string",
									"value": "kg"
								},
								{
									"name": "value",
									"type": "decimal",
									"value": "1.900"
								}
							]
						}
					},
					{
						"name": "transportStart",
						"record": {
							"subrecords": [
								{
									"name": "postalAddress",
									"record": {
										"fields": [
											{
												"name": "countryIsoCode",
												"type": "string",
												"value": "DE"
											},
											{
												"name": "postcode",
												"type": "string",
												"value": "70597"
											}
										]
									}
								}
							]
						}
					},
					{
						"name": "transportEnd",
						"record": {
							"subrecords": [
								{
									"name": "postalAddress",
									"record": {
										"fields": [
											{
												"name": "countryIsoCode",
												"type": "string",
												"value": "DE"
											},
											{
												"name": "postcode",
												"type": "string",
												"value": "94405"
											}
										]
									}
								}
							]
						}
					},
					{
						"name": "packages",
						"record": {
							"fields": [
								{
									"name": "dangerousGoodsHandlingCode",
									"type": "string",
									"value": "NONE"
								},
								{
									"name": "packageReferenceNumber",
									"type": "string",
									"value": "package1"
								},
								{
									"name": "numberOfPackages",
									"type": "decimal",
									"value": "1"
								}
							],
							"subrecords": [
								{
									"name": "volume",
									"record": {
										"fields": [
											{
												"name": "unit",
												"type": "string",
												"value": "ccm"
											},
											{
												"name": "value",
												"type": "decimal",
												"value": "1500.000"
											}
										]
									}
								},
								{
									"name": "grossWeight",
									"record": {
										"fields": [
											{
												"name": "unit",
												"type": "string",
												"value": "kg"
											},
											{
												"name": "value",
												"type": "decimal",
												"value": "0.600"
											}
										]
									}
								},
								{
									"name": "dimensions",
									"record": {
										"fields": [
											{
												"name": "length",
												"type": "decimal",
												"value": "30.000"
											},
											{
												"name": "width",
												"type": "decimal",
												"value": "10.000"
											},
											{
												"name": "quantityUnit",
												"type": "string",
												"value": "cm"
											},
											{
												"name": "height",
												"type": "decimal",
												"value": "5.000"
											}
										]
									}
								}
							]
						}
					},
					{
						"name": "packages",
						"record": {
							"fields": [
								{
									"name": "dangerousGoodsHandlingCode",
									"type": "string",
									"value": "NONE"
								},
								{
									"name": "packageTypeIdentCode",
									"type": "string",
									"value": "packageType"
								},
								{
									"name": "packageReferenceNumber",
									"type": "string",
									"value": "package2"
								},
								{
									"name": "numberOfPackages",
									"type": "decimal",
									"value": "1"
								}
							],
							"subrecords": [
								{
									"name": "volume",
									"record": {
										"fields": [
											{
												"name": "unit",
												"type": "string",
												"value": "ccm"
											},
											{
												"name": "value",
												"type": "decimal",
												"value": "3000.000"
											}
										]
									}
								},
								{
									"name": "grossWeight",
									"record": {
										"fields": [
											{
												"name": "unit",
												"type": "string",
												"value": "kg"
											},
											{
												"name": "value",
												"type": "decimal",
												"value": "1.300"
											}
										]
									}
								},
								{
									"name": "dimensions",
									"record": {
										"fields": [
											{
												"name": "length",
												"type": "decimal",
												"value": "30.000"
											},
											{
												"name": "width",
												"type": "decimal",
												"value": "20.000"
											},
											{
												"name": "quantityUnit",
												"type": "string",
												"value": "cm"
											},
											{
												"name": "height",
												"type": "decimal",
												"value": "5.000"
											}
										]
									}
								}
							]
						}
					}
				]
			}
		}
	]
}
```
```xml
<createServiceItems>
	<request>
		<clientSystemId>APITEST</clientSystemId>
		<clientIdentCode>APITEST</clientIdentCode>
		<userName>user</userName>
		<resultLanguageIsoCodes>de</resultLanguageIsoCodes>
		<resultLanguageIsoCodes>en</resultLanguageIsoCodes>
		<parms>
			<calculatePriceImmediately>true</calculatePriceImmediately>
			<createSettlementsImmediately>false</createSettlementsImmediately>
			<returnTraceInfo>false</returnTraceInfo>
		</parms>
		<items>
			<itemId>25-11-2022</itemId>
			<scenarioIdentCode>A01</scenarioIdentCode>
			<serviceIdentCode>TNTDE_EXP12</serviceIdentCode>
			<referenceNumber>25-11-2022</referenceNumber>
			<orderNumber>25-11-2022</orderNumber>
			<serviceProvider>
				<companyNumber>TNT</companyNumber>
				<name>TNT Express Worldwide</name>
				<street>Heilbronner Staße 110</street>
				<postcode>70334</postcode>
				<city>Stuttgart</city>
				<countryISOCode>DE</countryISOCode>
			</serviceProvider>
			<orderer>
				<companyNumber>001</companyNumber>
				<name>AEB SE</name>
				<street>Sigmaringer Straße 109</street>
				<postcode>70567</postcode>
				<city>Stuttgart</city>
				<countryISOCode>DE</countryISOCode>
			</orderer>
			<payer>
				<companyNumber>001</companyNumber>
				<name>AEB SE</name>
				<street>Sigmaringer Straße 109</street>
				<postcode>70567</postcode>
				<city>Stuttgart</city>
				<countryISOCode>DE</countryISOCode>
			</payer>
			<beneficiary>
				<companyNumber>001</companyNumber>
				<name>AEB SE</name>
				<street>Sigmaringer Straße 109</street>
				<postcode>70567</postcode>
				<city>Stuttgart</city>
				<countryISOCode>DE</countryISOCode>
			</beneficiary>
			<referenceDate>
				<dateInTimezone>2022-11-25 12:00:00</dateInTimezone>
				<timezone>Europe/Berlin</timezone>
			</referenceDate>
			<pricingDate>
				<dateInTimezone>2022-11-25 12:00:00</dateInTimezone>
				<timezone>Europe/Berlin</timezone>
			</pricingDate>
			<chargeDate>
				<dateInTimezone>2022-11-25 12:00:00</dateInTimezone>
				<timezone>Europe/Berlin</timezone>
			</chargeDate>
			<serviceDate>
				<dateInTimezone>2022-11-25 12:00:00</dateInTimezone>
				<timezone>Europe/Berlin</timezone>
			</serviceDate>
			<orderDate>
				<dateInTimezone>2022-11-25 12:00:00</dateInTimezone>
				<timezone>Europe/Berlin</timezone>
			</orderDate>
			<quantity>
				<value>1</value>
				<unit>St</unit>
			</quantity>
			<description>Shipment</description>
			<extendedData>
				<fields>
					<name>carrierDefinitionIdentCode</name>
					<type>string</type>
					<value>TNT</value>
				</fields>
				<fields>
					<name>numberOfInvoices</name>
					<type>decimal</type>
					<value>1</value>
				</fields>
				<fields>
					<name>isDangerousGoods</name>
					<type>boolean</type>
					<value>false</value>
				</fields>
				<fields>
					<name>referenceNumber</name>
					<type>string</type>
					<value>referenceNumber</value>
				</fields>
				<fields>
					<name>incotermIdentCode</name>
					<type>string</type>
					<value>incoterm</value>
				</fields>
				<fields>
					<name>numberOfItems</name>
					<type>decimal</type>
					<value>2</value>
				</fields>
				<fields>
					<name>palletPlaces</name>
					<type>decimal</type>
					<value>1.000</value>
				</fields>
				<fields>
					<name>numberOfPackages</name>
					<type>decimal</type>
					<value>2</value>
				</fields>
				<fields>
					<name>isDocumentShipment</name>
					<type>boolean</type>
					<value>false</value>
				</fields>
				<fields>
					<name>numberOfDeliveryNotes</name>
					<type>decimal</type>
					<value>1</value>
				</fields>
				<subrecords>
					<name>volume</name>
					<record>
						<fields>
							<name>unit</name>
							<type>string</type>
							<value>ccm</value>
						</fields>
						<fields>
							<name>value</name>
							<type>decimal</type>
							<value>4500.000</value>
						</fields>
					</record>
				</subrecords>
				<subrecords>
					<name>grossWeight</name>
					<record>
						<fields>
							<name>unit</name>
							<type>string</type>
							<value>kg</value>
						</fields>
						<fields>
							<name>value</name>
							<type>decimal</type>
							<value>1.900</value>
						</fields>
					</record>
				</subrecords>
				<subrecords>
					<name>transportStart</name>
					<record>
						<subrecords>
							<name>postalAddress</name>
							<record>
								<fields>
									<name>countryIsoCode</name>
									<type>string</type>
									<value>DE</value>
								</fields>
								<fields>
									<name>postcode</name>
									<type>string</type>
									<value>70597</value>
								</fields>
							</record>
						</subrecords>
					</record>
				</subrecords>
				<subrecords>
					<name>transportEnd</name>
					<record>
						<subrecords>
							<name>postalAddress</name>
							<record>
								<fields>
									<name>countryIsoCode</name>
									<type>string</type>
									<value>DE</value>
								</fields>
								<fields>
									<name>postcode</name>
									<type>string</type>
									<value>94405</value>
								</fields>
							</record>
						</subrecords>
					</record>
				</subrecords>
				<subrecords>
					<name>packages</name>
					<record>
						<fields>
							<name>dangerousGoodsHandlingCode</name>
							<type>string</type>
							<value>NONE</value>
						</fields>
						<fields>
							<name>packageReferenceNumber</name>
							<type>string</type>
							<value>package1</value>
						</fields>
						<fields>
							<name>numberOfPackages</name>
							<type>decimal</type>
							<value>1</value>
						</fields>
						<subrecords>
							<name>volume</name>
							<record>
								<fields>
									<name>unit</name>
									<type>string</type>
									<value>ccm</value>
								</fields>
								<fields>
									<name>value</name>
									<type>decimal</type>
									<value>1500.000</value>
								</fields>
							</record>
						</subrecords>
						<subrecords>
							<name>grossWeight</name>
							<record>
								<fields>
									<name>unit</name>
									<type>string</type>
									<value>kg</value>
								</fields>
								<fields>
									<name>value</name>
									<type>decimal</type>
									<value>0.600</value>
								</fields>
							</record>
						</subrecords>
						<subrecords>
							<name>dimensions</name>
							<record>
								<fields>
									<name>length</name>
									<type>decimal</type>
									<value>30.000</value>
								</fields>
								<fields>
									<name>width</name>
									<type>decimal</type>
									<value>10.000</value>
								</fields>
								<fields>
									<name>quantityUnit</name>
									<type>string</type>
									<value>cm</value>
								</fields>
								<fields>
									<name>height</name>
									<type>decimal</type>
									<value>5.000</value>
								</fields>
							</record>
						</subrecords>
					</record>
				</subrecords>
				<subrecords>
					<name>packages</name>
					<record>
						<fields>
							<name>dangerousGoodsHandlingCode</name>
							<type>string</type>
							<value>NONE</value>
						</fields>
						<fields>
							<name>packageTypeIdentCode</name>
							<type>string</type>
							<value>packageType</value>
						</fields>
						<fields>
							<name>packageReferenceNumber</name>
							<type>string</type>
							<value>package2</value>
						</fields>
						<fields>
							<name>numberOfPackages</name>
							<type>decimal</type>
							<value>1</value>
						</fields>
						<subrecords>
							<name>volume</name>
							<record>
								<fields>
									<name>unit</name>
									<type>string</type>
									<value>ccm</value>
								</fields>
								<fields>
									<name>value</name>
									<type>decimal</type>
									<value>3000.000</value>
								</fields>
							</record>
						</subrecords>
						<subrecords>
							<name>grossWeight</name>
							<record>
								<fields>
									<name>unit</name>
									<type>string</type>
									<value>kg</value>
								</fields>
								<fields>
									<name>value</name>
									<type>decimal</type>
									<value>1.300</value>
								</fields>
							</record>
						</subrecords>
						<subrecords>
							<name>dimensions</name>
							<record>
								<fields>
									<name>length</name>
									<type>decimal</type>
									<value>30.000</value>
								</fields>
								<fields>
									<name>width</name>
									<type>decimal</type>
									<value>20.000</value>
								</fields>
								<fields>
									<name>quantityUnit</name>
									<type>string</type>
									<value>cm</value>
								</fields>
								<fields>
									<name>height</name>
									<type>decimal</type>
									<value>5.000</value>
								</fields>
							</record>
						</subrecords>
					</record>
				</subrecords>
			</extendedData>
		</items>
	</request>
</createServiceItems>
```
