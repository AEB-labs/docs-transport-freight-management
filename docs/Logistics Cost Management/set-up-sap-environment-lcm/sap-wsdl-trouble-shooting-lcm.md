---
title: SAP WSDL trouble shooting (LCM)
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
There are some known issues with importing an WSDL into SAP. 

* using reference other wsdl files
* using extension
* using recursion

The most errors are no issues with S/4HANA but with older SAP versions.

## Reference other WSDL files:

* Save the WSDL files locally (the second file is reference in the first file)
* fix the path between both files 

For example it looks like that:

```xml
<types>
<xsd:schema>
<xsd:import namespace="urn:de.aeb.xnsg.billing.bf" schemaLocation="https://rz3.aeb.de:443/test2billing/servlet/bf/BillingBF?xsd=1"/>
</xsd:schema>
</types>
```

Just fix that to :

```xml
<types>
<xsd:schema>
<xsd:import namespace="urn:de.aeb.xnsg.billing.bf" schemaLocation="localBillingBFxsd.xml"/>
</xsd:schema>
</types>
```

 \##Using extension\
In the XSD file there are all defined types. Some types uses the extension tag. This is not allowed from all SAP version. Just search vor the type which is referenced in the extension tag und copy the fields to the type which is using the extension.

Example:

```xml
<xs:complexType name="bReverseServiceItemsRequestDTO">
<xs:complexContent>
<xs:extension base="tns:abstractRequestDTO">
<xs:sequence>
<xs:element name="reasonOfReversal" type="xs:string" minOccurs="0"/>
<xs:element name="items" type="tns:bServiceItemReferenceDTO" nillable="true" minOccurs="0" maxOccurs="unbounded"/>
</xs:sequence>
</xs:extension>
</xs:complexContent>
</xs:complexType>
```

There referenced type looks like the following XML:

```xml
<xs:complexType name="abstractRequestDTO">
<xs:sequence>
<xs:element name="clientSystemId" type="xs:string" minOccurs="0"/>
<xs:element name="clientIdentCode" type="xs:string" minOccurs="0"/>
<xs:element name="userName" type="xs:string" minOccurs="0"/>
<xs:element name="resultLanguageIsoCodes" type="xs:string" nillable="true" minOccurs="0" maxOccurs="unbounded"/>
</xs:sequence>
</xs:complexType>
```

And without extension it looks like the following XML:

```xml
<xs:complexType name="bReverseServiceItemsRequestDTO">
<xs:complexContent>
<xs:sequence>
<xs:element name="clientSystemId" type="xs:string" minOccurs="0"/>
<xs:element name="clientIdentCode" type="xs:string" minOccurs="0"/>
<xs:element name="userName" type="xs:string" minOccurs="0"/>
<xs:element name="resultLanguageIsoCodes" type="xs:string" nillable="true" minOccurs="0" maxOccurs="unbounded"/>
<xs:element name="reasonOfReversal" type="xs:string" minOccurs="0"/>
<xs:element name="items" type="tns:bServiceItemReferenceDTO" nillable="true" minOccurs="0" maxOccurs="unbounded"/>
</xs:sequence>
</xs:complexContent>
</xs:complexType>
```

## Using recursion

we have to finalize the recursion so that we have an end and we have to replace the recursion with concrete Types like TypeArea1 reffers TypeArea2 reffers TypeArea3 and so on...\
Example:\
We have a type genericDataFieldDTO which reffers namedGenericDataRecordDTO this type reffers genericDataFieldDTO.. so the recursion starts... 

```xml
<xs:complexType name="genericDataRecordDTO">
<xs:sequence>
<xs:element name="fields" type="tns:genericDataFieldDTO" nillable="true" minOccurs="0" maxOccurs="unbounded"/>
<xs:element name="subrecords" type="tns:namedGenericDataRecordDTO" nillable="true" minOccurs="0" maxOccurs="unbounded"/>
</xs:sequence>
</xs:complexType>

<xs:complexType name="namedGenericDataRecordDTO">
<xs:sequence>
<xs:element name="name" type="xs:string" minOccurs="0"/>
<xs:element name="record" type="tns:genericDataRecord1DTO" minOccurs="0"/>
</xs:sequence>
</xs:complexType>
```

The fix is:

```xml
<xs:complexType name="genericDataRecordDTO">
<xs:sequence>
<xs:element name="fields" type="tns:genericDataFieldDTO" nillable="true" minOccurs="0" maxOccurs="unbounded"/>
<xs:element name="subrecords" type="tns:namedGenericDataRecordDTO" nillable="true" minOccurs="0" maxOccurs="unbounded"/>
</xs:sequence>
</xs:complexType>

<xs:complexType name="namedGenericDataRecordDTO">
<xs:sequence>
<xs:element name="name" type="xs:string" minOccurs="0"/>
<xs:element name="record" type="tns:genericDataRecord1DTO" minOccurs="0"/>
</xs:sequence>
</xs:complexType>

<xs:complexType name="namedGenericDataRecord1DTO">
<xs:sequence>
<xs:element name="name" type="xs:string" minOccurs="0"/>
<xs:element name="record" type="tns:genericDataRecord2DTO" minOccurs="0"/>
</xs:sequence>
</xs:complexType>

<xs:complexType name="genericDataRecord1DTO">
<xs:sequence>
<xs:element name="fields" type="tns:genericDataFieldDTO" nillable="true" minOccurs="0" maxOccurs="unbounded"/>
<xs:element name="subrecords" type="tns:namedGenericDataRecord1DTO" nillable="true" minOccurs="0" maxOccurs="unbounded"/>
</xs:sequence>
</xs:complexType>

<xs:complexType name="genericDataRecord2DTO">
<xs:sequence>
<xs:element name="fields" type="tns:genericDataFieldDTO" nillable="true" minOccurs="0" maxOccurs="unbounded"/>
</xs:sequence>
</xs:complexType>
```

So now it looks like:\
genericDataRecordDTO -> namedGenericDataRecordDTO -> genericDataRecord1DTO -> namedGenericDataRecord1DTO -> genericDataRecord2DTO (the last record stops with th recursio)
