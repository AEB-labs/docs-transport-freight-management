---
title: Document Templates
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
# Overview

The document preparation consists of merging of a predefined layout template, available in the Document Service, with customer data, transmitted in a webservice call. The following <<glossary:Document template>> _types_ are available:

## Adobe PDF-XFA Forms

Adobe PDF-XFA Forms are based on the PDF-XFA technology. The template files are designed by _Adobe Experience Manager_ (or, previously, _Life Cycle Designer_). Although the template is saved as a \*.pdf file, it contains just a PDF header as an envelope that embeds the actual XDP content with the XFA layout specification. It should not be confused with ordinary PDF documents.

The XFA layout allows you to design forms and reports with dynamically growing areas, nested loops and tables and controllable page overflows. Image data and common barcodes are supported as well.

The templates are handled by the `PDF-XFA` <<glossary:Document processor>>. Only a limited set of XFA features and a couple of non-standard extension is supported. Therefore it is crucial that the templates forms are prepared by AEB experts.

## NiceLabel

NiceLabel template files are proprietary (license required). They are designed by _NiceLabel Designer_ and usually saved as \*.nlbl files.

The NiceLabel templates allow to design rectangular forms with positioned fields. Many barcodes are supported. The templates are printer-independent.

# Additional Template Resources

The individual document templates usually come along with some other accompanying resources, e.g.:

- Document data structure (XSD Schema). The data to be merged with the template must conform to this structure.
- Example data. Either predefined or empty data examples are available for faster learning and easier testing.
- Translation texts. It is possible to design multi-language templates. The translation texts are available in separate files (one per language).

# Try it out

## Explore the Templates

It's time to [get the <<glossary:Document template>>s](/reference/querydocumenttemplates) that are available in your context.

You can obtain a list of templates in this form:

```json
{
  "infos": [
    {
      "filename": "DemoDoc10.pdf",
      "processor": "PDF-XFA",
      "isStandard": true,
      "isCustomized": false,
      "isClientCustomized": false,
      "isManagedExternally": false
    }
  ]
}
```

Each template is uniquely identified by its `filename`. Besides the standard templates (identifiable by `"isStandard": true`), it is also possible to have client-specific customization of the standard templates or completely new custom templates. Client-specific customizations override the corresponding standard templates with identical file names.

## Get some Example Data

Now you'd certainly like to now what **data** can be merged with each template. The templates are usually accompanied by one or more data example files. You can try to [get them](/reference/parsedocumenttemplatecontent). You need to fill-in the required template file name, the corresponding processor type and `XMLs` as the `query` value.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a72c473-image.png",
        null,
        ""
      ],
      "align": "center",
      "border": true
    }
  ]
}
[/block]

(Note that "XMLs" is one of the `supportedParseCommands` explained in the [previous](doc:document-processors) chapter.)

You get a plain text with list of example file names that accompany the template:

```
DemoDoc10.example.xml

```

### Templates with Examples

If there are **any examples** in the response, choose one and apply the name to [download it](/reference/parsedocumenttemplatecontent).  You need to fill-in the required template file name, the corresponding processor type again and `XML?DemoDoc10.example.xml` as the `query` value (of course, instead of "DemoDoc10.example.xml", use the example file name you have chosen).

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c8c5b0a-image.png",
        null,
        ""
      ],
      "align": "center",
      "border": true
    }
  ]
}
[/block]

You get some _XML content_ with a `documentData` root element, containing the example data.

```xml
<documentData>
	...
</documentData>
```

Copy the data and save it to a file (named e.g. "DemoDoc10.example.xml"). Please be careful with the charset encoding - sometimes the data gets corrupted during manual manipulation. A better way is to directly save the content from the request.

If you use the [Swagger UI](https://rz3.aeb.de/demo1docs/swagger/#/DocumentService/parseDocumentTemplateContent), it offers a "download" link that saves the data directly to a file.

You can also [download](https://rz3.aeb.de/demo1docs/rest/DocumentService/template/DemoDoc10.pdf/parse?processor=PDF-XFA&query=XML%3FDemoDoc10.example.xml) and save the "DemoDoc10.example.xml" file with a direct link.

### Templates without Examples

If there are **no predefined examples**, you can still [download an empty example](/reference/parsedocumenttemplatecontent).  You need to fill-in the required template file name, the corresponding processor type again and use just `XML` as the `query` value.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/b02152e-image.png",
        null,
        ""
      ],
      "align": "center",
      "border": true
    }
  ]
}
[/block]

You also get _XML content_ with a `documentData` root element containing all fields that are supported in the template, filled with the `?` value. You can replace the `?` with your own data (note that you have to stick to the XML syntax, so take care and escape the special characters like `<`, `>`, `&` etc. accordingly). Binary images (PNG, JPG) must be Base64 encoded. Some complex barcodes also require Base64 encoded binary data.

You can also [download](https://rz3.aeb.de/demo1docs/rest/DocumentService/template/DemoDoc10.pdf/parse?processor=PDF-XFA&query=XML) and save the empty data file for the "DemoDoc10" template with a direct link.

When you have an example now, you can skip the next paragraph and jump directly to the [document preparation](doc:document-preparation).

## Document Schema

For a complete understanding of the template data structure, [get the <<glossary:Document schema>>](/reference/parsedocumenttemplatecontent) . You need to fill-in the required template file name, the corresponding processor type and `XSD` as the `query` value.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/992fa36-image.png",
        null,
        ""
      ],
      "align": "center",
      "border": true
    }
  ]
}
[/block]

(Note that "XSD" is also one of the `supportedParseCommands` explained in the [previous](doc:document-processors) chapter.)

You get a valid _XML Schema Description_ content back:

```xml
<?xml version='1.0' encoding='UTF-8'?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" id="XFASchemaXSD">
    <xs:element name="documentData" type="DocumentData"/>
    <xs:complexType name="DocumentData">
        <xs:sequence>
            <xs:element name="DocumentTitle" type="xs:string"/>
            <xs:element name="Logo_Center" type="xs:string"/>
            <xs:element name="Logo_Right" type="xs:string"/>
            <xs:element name="Adress_1" type="Adress"/>
            <xs:element name="Adress_2" type="Adress"/>
            <xs:element name="Footer_Left" type="xs:string"/>
            <xs:element name="Footer_Center" type="xs:string"/>
            <xs:element name="Footer_Right" type="xs:string"/>
            <xs:element maxOccurs="unbounded" name="Reference_Loop" type="Loop1_type"/>
            <xs:element name="Content" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
    <xs:complexType name="Adress">
        <xs:sequence>
            <xs:element name="Address_Name" type="xs:string"/>
            <xs:element name="Address" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
    <xs:complexType name="Loop1_type">
        <xs:sequence>
            <xs:element name="Reference" type="Reference_type"/>
        </xs:sequence>
    </xs:complexType>
    <xs:complexType name="Reference_type">
        <xs:sequence>
            <xs:element name="Reference_Name" type="xs:string"/>
            <xs:element name="Reference_Text" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:schema>
```

You can use this schema to generate valid XML data that can be used to fill-in this template and thus create a document content from the template.