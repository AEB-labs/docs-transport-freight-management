---
title: Output Settings
excerpt: >-
  Description of configuration settings relevant for document print, preview,
  editing and archiving.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Purpose and Use

During the document generation, printing, archiving etc., some accompanying settings or parameters are often required. For the [staged document instances](doc:staged-document-instances), these parameters are **not** part of the API requests — they need to be maintained manually and are stored in the system together with other *master data*. The parameters are referenced to as *output settings*.

The output settings can be maintained individually for each <Glossary>Document type</Glossary> or predefined separately under a symbolic name and then reused as a *default preset* in several document types at once. There is always a default preset called "Standard".

The output settings can be supplemented or overloaded for specific contexts: *client*, *workstation* and *user* (the settings are inherited in this order). The current valid context (or scope) depends on the session properties. In API requests, it is determined by the authentication data by default. When applicable, the *workstation* can be optionally specified in the request payload data (look after a field called `workstationId`).

# Settings overview

The central application for the settings is to be found in the *Office* under *Master data* — *Documents - output settings*:

![](https://files.readme.io/ea45852-image.png)There, the target settings container and scope can be easily selected. Default, inherited settings are displayed in *italic* in the description. Overloaded values are displayed in **bold**.The individual *workstations* can be configured in *Master data* — *Workstations*. Workstations are meant to be used when you need different settings for specific locations or use cases that are neither common for all your users nor specific to a single user.

# Typical Settings

## Default printer

The client printers are provided externally by the *AEB Cloud Printing Service*, which is installed at your location and connected to the *Document Service*. In consequence, all users "see" the same list of printers and the default printer provided by the cloud printing service.

Using the output settings, the default printer can be overloaded with own preferences for any user or workstation context.

When you modify it in the "Standard" settings, it is then inherited in all other settings and document types.

### Logical printer

If you need to specify different default printers for individual document types  (or groups of document types), you can also create new settings with symbolic names like "Laserprinter", "Thermoprinter" etc. and proceed with the user or workstation settings as described above.

Then you apply the new settings as *default preset* for the selected document types: open the document type record and select the *Default* settings from the combo box (it becomes the "parent" settings for the document type).

## NiceLabel printers

The *NiceLabel* documents require additional *printer type* settings (for both the generating and printing of the document). For this reason, only **preconfigured printers** (see  *Master data* — *Printers*) are allowed to be used in the settings.

The concept of logical printers described above can be applied to this situation.

## PDF formats

The *PDF-XFA* <Glossary>Document processor</Glossary> can generate documents in [various formats](doc:document-processors#pdf-xfa). By default, the format for *preview* is **PDF** (PDF 1.5 with layers) and the format for *print* is **PDFa** (PDF/a). Thus, two contents are generated for each document.

For documents that are designed to be printed on preprinted forms, the format **PDFa data** would be required for printing, whereas the preview can still make use of the **PDF** format, where the background layer is visible, too (and can be optionally hidden when you download the document and open it in the Adobe Reader).

If archiving is enabled, both formats are archived, too.

In the output settings for each corresponding action, you can select the required format (or formats).

## Disable editing

The data of *PDF-XFA* documents can be, in general, edited in a WYSIWYG document editor. However, for some documents it might be undesirable to allow the content modification:

* document manipulation is restricted due to security reasons or to ensure consistency with data provided by the master system
* the document is rather a "report" than a "form" and it is not meant to be changeable at all (huge documents are also difficult to edit and can cause performance issues)

You can disable it in the output settings *for editing*.
