---
title: SAP WSDL trouble shooting
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

- using reference other wsdl files
- using recursion
- using exentsion 

The most errors are no issues with S/4HANA but with older SAP versions.

**Reference other WSDL files:**
- Save the WSDL files locally (the second file is reference in the first file)
- fix the path between both files 

For example it looks like that:
[block:code]
{
  "codes": [
    {
      "code": "<types>\n<xsd:schema>\n<xsd:import namespace=\"urn:de.aeb.xnsg.billing.bf\" schemaLocation=\"https://rz3.aeb.de:443/test2billing/servlet/bf/BillingBF?xsd=1\"/>\n</xsd:schema>\n</types>",
      "language": "xml"
    }
  ]
}
[/block]
Just fix that to :
[block:code]
{
  "codes": [
    {
      "code": "<types>\n<xsd:schema>\n<xsd:import namespace=\"urn:de.aeb.xnsg.billing.bf\" schemaLocation=\"localBillingBFxsd.xml\"/>\n</xsd:schema>\n</types>",
      "language": "xml"
    }
  ]
}
[/block]
 **Using extension**
In the XSD file there are all defined types. Some types uses the extension tag. This is not allowed from all SAP version. Just search vor the type which is referenced in the extension tag und copy the fields to the type which is using the extension.

Example:
[block:code]
{
  "codes": [
    {
      "code": "<xs:complexType name=\"bReverseServiceItemsRequestDTO\">\n<xs:complexContent>\n<xs:extension base=\"tns:abstractRequestDTO\">\n<xs:sequence>\n<xs:element name=\"reasonOfReversal\" type=\"xs:string\" minOccurs=\"0\"/>\n<xs:element name=\"items\" type=\"tns:bServiceItemReferenceDTO\" nillable=\"true\" minOccurs=\"0\" maxOccurs=\"unbounded\"/>\n</xs:sequence>\n</xs:extension>\n</xs:complexContent>\n</xs:complexType>",
      "language": "xml"
    }
  ]
}
[/block]
There referenced type looks like the following XML:
[block:code]
{
  "codes": [
    {
      "code": "<xs:complexType name=\"abstractRequestDTO\">\n<xs:sequence>\n<xs:element name=\"clientSystemId\" type=\"xs:string\" minOccurs=\"0\"/>\n<xs:element name=\"clientIdentCode\" type=\"xs:string\" minOccurs=\"0\"/>\n<xs:element name=\"userName\" type=\"xs:string\" minOccurs=\"0\"/>\n<xs:element name=\"resultLanguageIsoCodes\" type=\"xs:string\" nillable=\"true\" minOccurs=\"0\" maxOccurs=\"unbounded\"/>\n</xs:sequence>\n</xs:complexType>",
      "language": "xml"
    }
  ]
}
[/block]
And without extension it looks like the following XML:
[block:code]
{
  "codes": [
    {
      "code": "<xs:complexType name=\"bReverseServiceItemsRequestDTO\">\n<xs:complexContent>\n<xs:sequence>\n<xs:element name=\"clientSystemId\" type=\"xs:string\" minOccurs=\"0\"/>\n<xs:element name=\"clientIdentCode\" type=\"xs:string\" minOccurs=\"0\"/>\n<xs:element name=\"userName\" type=\"xs:string\" minOccurs=\"0\"/>\n<xs:element name=\"resultLanguageIsoCodes\" type=\"xs:string\" nillable=\"true\" minOccurs=\"0\" maxOccurs=\"unbounded\"/>\n<xs:element name=\"reasonOfReversal\" type=\"xs:string\" minOccurs=\"0\"/>\n<xs:element name=\"items\" type=\"tns:bServiceItemReferenceDTO\" nillable=\"true\" minOccurs=\"0\" maxOccurs=\"unbounded\"/>\n</xs:sequence>\n</xs:complexContent>\n</xs:complexType>",
      "language": "xml"
    }
  ]
}
[/block]
**Using recursion**
we have to finalize the recursion so that we have an end and we have to replace the recursion with concrete Types like TypeArea1 reffers TypeArea2 reffers TypeArea3 and so on...
Example:
We have a type genericDataFieldDTO which reffers namedGenericDataRecordDTO this type reffers genericDataFieldDTO.. so the recursion starts... 

[block:code]
{
  "codes": [
    {
      "code": "<xs:complexType name=\"genericDataRecordDTO\">\n<xs:sequence>\n<xs:element name=\"fields\" type=\"tns:genericDataFieldDTO\" nillable=\"true\" minOccurs=\"0\" maxOccurs=\"unbounded\"/>\n<xs:element name=\"subrecords\" type=\"tns:namedGenericDataRecordDTO\" nillable=\"true\" minOccurs=\"0\" maxOccurs=\"unbounded\"/>\n</xs:sequence>\n</xs:complexType>\n\n<xs:complexType name=\"namedGenericDataRecordDTO\">\n<xs:sequence>\n<xs:element name=\"name\" type=\"xs:string\" minOccurs=\"0\"/>\n<xs:element name=\"record\" type=\"tns:genericDataRecord1DTO\" minOccurs=\"0\"/>\n</xs:sequence>\n</xs:complexType>\n\n",
      "language": "xml"
    }
  ]
}
[/block]
The fix is:
[block:code]
{
  "codes": [
    {
      "code": "<xs:complexType name=\"genericDataRecordDTO\">\n<xs:sequence>\n<xs:element name=\"fields\" type=\"tns:genericDataFieldDTO\" nillable=\"true\" minOccurs=\"0\" maxOccurs=\"unbounded\"/>\n<xs:element name=\"subrecords\" type=\"tns:namedGenericDataRecordDTO\" nillable=\"true\" minOccurs=\"0\" maxOccurs=\"unbounded\"/>\n</xs:sequence>\n</xs:complexType>\n\n<xs:complexType name=\"namedGenericDataRecordDTO\">\n<xs:sequence>\n<xs:element name=\"name\" type=\"xs:string\" minOccurs=\"0\"/>\n<xs:element name=\"record\" type=\"tns:genericDataRecord1DTO\" minOccurs=\"0\"/>\n</xs:sequence>\n</xs:complexType>\n\n<xs:complexType name=\"namedGenericDataRecord1DTO\">\n<xs:sequence>\n<xs:element name=\"name\" type=\"xs:string\" minOccurs=\"0\"/>\n<xs:element name=\"record\" type=\"tns:genericDataRecord2DTO\" minOccurs=\"0\"/>\n</xs:sequence>\n</xs:complexType>\n\n<xs:complexType name=\"genericDataRecord1DTO\">\n<xs:sequence>\n<xs:element name=\"fields\" type=\"tns:genericDataFieldDTO\" nillable=\"true\" minOccurs=\"0\" maxOccurs=\"unbounded\"/>\n<xs:element name=\"subrecords\" type=\"tns:namedGenericDataRecord1DTO\" nillable=\"true\" minOccurs=\"0\" maxOccurs=\"unbounded\"/>\n</xs:sequence>\n</xs:complexType>\n\n<xs:complexType name=\"genericDataRecord2DTO\">\n<xs:sequence>\n<xs:element name=\"fields\" type=\"tns:genericDataFieldDTO\" nillable=\"true\" minOccurs=\"0\" maxOccurs=\"unbounded\"/>\n</xs:sequence>\n</xs:complexType>",
      "language": "xml"
    }
  ]
}
[/block]
So now it looks like:
genericDataRecordDTO -> namedGenericDataRecordDTO -> genericDataRecord1DTO -> namedGenericDataRecord1DTO -> genericDataRecord2DTO (the last record stops with th recursio)