---
title: Document Processors
excerpt: Introduction to document processing types available in the Document Service
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

The document preparation consists of merging of a predefined <<glossary:Document template>>s, available in the _Document Service_, with customer data, transmitted in a customer request. The following <<glossary:Document processor>>s are available:

## PDF-XFA

This processor handles PDF Forms based on the XFA standard. Flat PDF files are generated from the template form. However, only a limited set of XFA features and a couple of non-standard extension is supported. Therefore it is crucial that the templates forms are prepared by experts from the _AEB document community_.

The following output formats are available:

- **PDF**: PDF 1.5 with layers: layout, data. The layout layer usually represents the pre-printed contents of forms or letterhead papers. In Adobe Reader you can hide the layout layer if necessary and so you can preview the document with as well as without the background layout and print it manually on the pre-printed form or a blank paper as it is needed. Suitable for preview, manual printing (optionally with or without background layout) and e-distribution. Note that other PDF viewers than Adobe Reader might not support the layer separation.
- **PDF print data**: PDF 1.5 with layers: layout, data. In Adobe Reader you can see the background and data, but when printing only the data is put out (also shown in print preview like this). Suitable for preview, manual printing on pre-printed forms (without need to remember to hide the layout layer manually). Note that other PDF viewers than Adobe Reader might not support the layer separation.
- **PDFa**: PDF/a with merged data and layout. Suitable for direct printing on white paper and archiving.
- **PDFa data**: PDF/a with data only (without layout). Suitable for direct printing on pre-printed forms or letterhead papers and archiving.

## NiceLabel

This processor uses a third party proprietary application to generate variety of labels for direct and efficient printing on common thermal printers. The list of supported printer types is limited.

The following output formats are available:

- Typically, **EPL** or **ZPL** printing language is used in the output (suitable for direct, raw printing to a compatible printer). The actual content depend on the applied printer driver.
- It is also possible to generate the label in **PDF** format (suitable for preview and archiving).

# Try it out

[Get <<glossary:Document processor tag>>s](/reference/getsupportedprocessors) available in your context.

The returned codes (tags) can be subsequently used in other calls to identify the target document processor.

Typically, you get an answer like this:

```json
{
  "supportedProcessors": [
    "PDF-XFA"
  ]
}
```

If you have arranged a license for labels with the AEB, you get:

```json
{
  "supportedProcessors": [
    "PDF-XFA",
    "NICELABEL"
  ]
}
```

Now you can [get supported processor functions & features](/reference/getprocessorinfo) for a processor. The returned values can be used in other calls to identify the target document output format or to extract information from the individual document templates.

For the `PDF-XFA` processor, you get an answer similar to this one:

```json
{
  "supportedFormats": [
    "PDF",
    "PDF data",
    "PDF print data",
    "PDFa",
    "PDFa data",
  ],
  "supportedProcessingParameters": [
    {
      "name": "PageOffsets"
    },
    {
      "name": "ContentVariant"
    }
  ],
  "supportedParseCommands": [
    "PageNames",
    "XFAForm",
    "XSD",
    "XML",
    "TextPlaceholders",
    "XMLs"
  ]
}
```

Not all of the values are relevant or important for you. Usage for some of them is illustrated in other chapters. Examples:

- One of the `supportedFormats` values can be used to specify the desired <<glossary:Document content>> output format when a document is prepared.
- The `supportedParseCommands` can be used to extract derived or additional content from the <<glossary:Document template>>, like the data structure or example documents.
- For the `NICELABEL` processor, you can get a list of the supported printer type names from the `supportedProcessingParameters`.