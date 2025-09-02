---
title: UPS
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
---
> 📘 Hinweise = /callout - Info

<Callout icon="💡" theme="default">
  ### Tipp = diesen Abschnitt kopieren
</Callout>

* Überschriften: Carrier Connect Use Cases
* Feldnamen: **documentOutputMode**
* Feldinhalte: `RETURN`

> 📘 Wenn es Sinn macht, Begriffe per Glossar erklären.

```json JSON
```
```xml
```

# Implementation information

EDI / webservice format?

Label formats, label documentation version

The package number and the total number of packages are usually printed on the package label, e.g. 1 OF 2 for the first package, 2 OF 2 for the second package. Exception is the UPS service "Standard Package". With this service, 1 OF 1 is always printed on each package label, regardless of how many packages there are in total in the shipment.\
If single package handling is activated, 1 OF *, 2 OF* , etc. will be printed on the label for all services except "UPS Standard Package".

**Understanding of domestic shipments**

For a domestic shipment, the shipper in the "Carrier configurations" account must be from the same country as the shipping point in the shipping order, otherwise UPS will not recognize it as a domestic shipment and an error message will occur when sending the EDI. Example: in the "Carrier configurations" account there is an address in NL, the customer's headquarters. The customer creates a shipping order and sends goods from his Swiss branch to a customer in Switzerland. This is a national shipment. But UPS does not allow it like this. There is an error message when sending the EDI regarding a missing \*CA06 address. The customer has to request a separate UPS account number from UPS for his Swiss branch and then set up an account for Switzerland in the "Carrier configurations".

# Required fields

Please check \[link] for general Carrier Connect required data.

Additionally the following data is required:

# Extra fields / additional values

# Logistics processes in detail

**Dangerous goods**

In the "Carrier configurations" in the account, the web service connection must be set up. Per customer, user-specific access data is required, which is provided by UPS.

For on-premises installations, you must remember to activate the firewall and proxy. The partner server entries are available and activated in the AEB data center.

processAcceptanceAuditPreCheck	\
this web service is triggered and executed in the background during label printing. UPS receives advance notice of dangerous goods shipments with it\
the contents of the web service requests and responses can be viewed via the logs of the business facades calls\
a partner server connection must be made for this web service, see section UPS Partner Server Connection\
processPreNotification	\
this web service is performed after the web service 'processAcceptanceAuditPreCheck'". UPS is thus notified in advance of the dangerous goods to be transported in the shipping orders\
the contents of the web service requests and responses can be viewed via the logs of the business facades calls\
a partner server connection must be made for this web service, see section UPS Partner Server Connection

For above mentioned web services access data are required, which are to be entered in the account in the "Carrier configuration". The customer can generate his own access data:

Access the following UPS page: [https://www.ups.com/de/de/Home.page](https://www.ups.com/de/de/Home.page)\
Register with new user name (the user name must not be identical with the user name for the PLD-Certification Tool)\
Register customer number for the new user\
After logging in to the UPS homepage with the new user, the new customer number must be registered:\
Unfold username in the upper right corner, select 'Payment Options'\
Select 'Add existing customer number'. For verification an invoice is required, which must not be older than 45 days\
Contrary to the default, enter the date in the format dd/mm/yyyy\
Access UPS Kit for Developers via the following link: [https://www.ups.com/upsdeveloperkit?loc=de\_DE](https://www.ups.com/upsdeveloperkit?loc=de_DE)\
Perform 'Step 4: Request an access key\
Enter the access key together with the username and password in the account

Please note: Dangerous goods must be packed to be treated as dangerous goods!

What is implemented?\
Implemented since FP 05/2017:

fully regulated dangerous goods\
EQ - excepted quantity\
LQ - limited quantity\
Lithium batteries (SP 07/2019, important corrections SP 01/2020 and FP 02/2020)\
Dry ice (from FP 08/2020)

The following dangerous goods have not yet been implemented:

Biological substances\
Genetically modified substances\
Exempted radioactive substances (SDA/11/2019: will not be transported by UPS, customer has to check with UPS).\
Special provisions\
To be entered in the dangerous goods item in the "Special provision" field

188	SP 03/2020	ADR	only valid for Lithiumbatteries\
283	SP 06/2021	ADR	\
371	SP 06/2021	ADR	\
594	SP 06/2021	ADR	\
A114	FP 05/2020	IATA	\
Packing instructions (IATA)\
To be entered in the dangerous goods item in the IATA folder in the "Packing instruction" field

965, Section IA	SP 03/2020	only valid for Lithiumbatteries\
965, Section IB	SP 03/2020	only valid for Lithiumbatteries\
965, Section II	SP 03/2020	only valid for Lithiumbatteries\
966, Section I	SP 03/2020	only valid for Lithiumbatteries\
966, Section II	SP 03/2020	only valid for Lithiumbatteries\
967, Section I	SP 03/2020	only valid for Lithiumbatteries\
967, Section II	SP 03/2020	only valid for Lithiumbatteries\
968, Section IA	SP 03/2020	only valid for Lithiumbatteries\
968, Section IB	SP 03/2020	only valid for Lithiumbatteries\
968, Section II	SP 03/2020	only valid for Lithiumbatteries\
969, Section I	SP 03/2020	only valid for Lithiumbatteries\
969, Section II	SP 03/2020	only valid for Lithiumbatteries\
970, Section I	SP 03/2020	only valid for Lithiumbatteries\
970, Section II	SP 03/2020	only valid for Lithiumbatteries\
Webservices for Dangerous Goods\
Partnerserver and Server connections see Webservices for Dangerous Goods above

For information: the web services for UPS dangerous goods are set up in our data center. Only if the customer has Carrier Connect with him, the web services must be set up and enabled in firewall/proxy, etc.

Settings for Dangerous Goods in the account\
In the "Carrier configuratons" in the UPS account, there is the Web Service Parameters section. Note here:

the customer must sign a contract with UPS about the dangerous goods\
User name, password and access key must be generated by the customer, see above

**Trade document upload**

Partner server connection: Paperless Document API\
In the "Carrier configurations" in the account, the web service connection must be set up. Per customer, user-specific access data is required, which is provided by UPS.

For on-premises installations, you must remember to activate the firewall and proxy. The partner server entries are available and activated in the AEB data center.

With this value added service the upload of documents is possible. The following document types can be uploaded:

002 - Commercial Invoice\
003 - Certificate of Origin\
004 - Export Accompanying Document (ABD)\
008 - Other\
010 - Packing List

Combination with World Ease is possible from SP02/2022!

The upload will be done when the shipping order is completed. A cancellation is not possible. However, the shipping order can be corrected and the documents uploaded again. With dispatch of the EDI no more change is possible.

Please note:

To upload documents, the additional service "Trade Document Upload" must be activated.\
If a COMMERCIAL\_INVOICE is uploaded, the additional service "Paperless Invoice" or "Paperless Invoice (Additional documents)" must NOT be activated.\
If one of the other implemented documents is uploaded, the additional service "Paperless Invoice (Additional documents)" must be activated.\
If the invoice should be created by UPS, only the additional service  "Paperless Invoice" must be activated.\
It's not possible to combine the upload of the COMMERCIAL\_INVOICE with other documents!\
Maximum values\
File size per file: 10 MB\
Total data size all files: 50 MB\
Number of files:\
maximum 13 files per request\
maximum 13 documents per file\
maximum 13 documents per shipment / shipping order\
Allowed formats\
3-digit: bmp, doc, gif, jpg, pdf, png, rtf, tif, txt und xls

4-digit: docx, xlsx

To note\
To determine the document type when uploading, the following text must be entered in the Comment field in the properties:

002	Commercial Invoice	COMMERCIAL\_INVOICE\
003	Certificate of Origin	CERTIFICATE\_OF\_ORIGIN\
004	Export Accompanying Document	EXPORT\_ACCOMPANYING\_DOCUMENT\
008	Other Document	OTHER\
010	Packing List	PACKING\_LIST\
Webservices for Paperless Document API\
Partnerserver and Server connections see Webservices for Paperless Document API above

**UPS WorldEase**

UPS World Ease allows multiple shipments destined for one country to be consolidated into a single consolidated shipment. In this case, a consolidated shipment is cleared by an appointed importer in the receiving country, who is responsible for paying duties and taxes. Where goods destined for one or more locations within the EU are to be exported from a third country, UPS can simplify the process by arranging for an EU country to serve as the point of entry.

World Ease is not available for shipments between EU countries

Implemented since FP05/2019

Please note: The adaptation effort for World Ease in connection with Carrier Connect and NSG ASSIST4 is high! It is advisable to carry out a detailed analysis and coordination of the processes required by the customer beforehand and to bill the customer for the time required. GS Stuttgart has experience in this area; if necessary, contact them in advance!

General requirements\
For each customer a separate POE file is generated by UPS (CSV file). This file must be read in the "Carrier configurations" at the customer in the "POE Zones Lists" folder. Description to POE see below\
The account number of the importer is mandatory. The entry is made:\
Master data / companies\
Open company, folder "Package processing"\
Carrier UPS, enter account number in the corresponding field (maximum 6 digits)\
All shipments (master and child) must have the same shipping date\
All shipments must have the same billing option\
No other services are allowed with the service "Standard", i.e. all shipments must use the service "Standard"\
General process overview\
image2020-11-16\_17-8-9.png

Requirements Master-Shipment\
The importer must be entered in the master shipment as the recipient. This is done automatically when creating the master-shipment from the child-shipment, provided that the importer is filled in the child\
The master-shipment must be a document shipment\
A maximum of one package is allowed in the master-shipment\
The "World Ease® Master" value added service must be set in the master-shipment\
Requirements Child-Shipment\
All child-shipments must use the same clearance port as the master-shipment\
All child-shipments must use the same importer\
All child shipments must be goods shipments\
The currency for all child-shipments must be identical, e.g. EUR everywhere\
The unit of weight for all child-shipments must be identical. As of 08/2019 only KGS is implemented\
All child-shipments within a master-shipment for UPS Expedited and UPS Standard (Package and Shipment) must contain the same service level. The allowed service level can be seen in the POE file\
The value added service "World Ease® Child" must be set in the child shipment\
Not allowed for World Ease\
Dangerous Goods (as of November 2019, dangerous goods are allowed)\
All UPS Return Services\
UPS package types Letter, 10KG BOX and 25KG BOX are not allowed in child-Shipments.\
Document-shipments are not allowed for child-shipments\
World Ease in connection with Trade document upload\
The value added service Trade document upload can be used in combination with World Ease, but only in combination with Paperless Invoice, i.e. variant 2 and variant 3, see below. This excludes an upload of the commercial invoice. The upload of documents is only possible in the child shipments, not in the master shipment.

The upload of documents for collective customs clearance is not provided by UPS in combination with World Ease or as an exception only in a special process which requires an internal approval procedure. UPS assumes that the customs relevant data will normally be uploaded via EDI and that the customer will provide a blank letterhead on which (upon request) a printout can be made as a customs invoice. As a rule, however, this is all handled electronically.

POE File\
In the World Ease application process, UPS agrees with the individual customer which destinations with which service types the customer requires. From this, the so-called Point of Entry (POE) table is created and sent to the customer as a CSV file. In this way, each customer receives their own POE file. When the label is printed, a POE address is determined from the POE table based on the data (UPS customer number, country, postal code and service type). For each row of the POE table used for the World Ease shipment, a separate master-shipment must be created - all associated child-shipments must be subordinate under this one. The address of the consignee is relevant for the POE table. The POE file is imported into the customer's "Carrier configurations".

File structure\
Encoding: UTF-8; Windows CR LF\
The file has 17 columns in row 1 (including POE number in last column) and 16 columns in all other rows\
It may happen that the last column contains "undefined". This column ("undefined") should be completely replaced by an empty value\
This looks in Notepad++ as follows:\
image2022-4-4\_22-13-37.png

Furthermore, the line end must be formatted in Windows (CR+LF). This can be set in the footer in Notepad++ with the right mouse button or under Edit >> Format line end.

image2022-4-4\_22-11-20.png

image2022-4-4\_22-11-12.png

Known errors\
Error: Line 2, record type POEZONE: record does not have the correct number of fields. Actual value: 1, target value: 16.

This indicates that the file is coded in Unix. Please change to Windows (CR+LF), see screenshot directly above.

Servicelevel\
The POE file lists the services that are allowed for the respective customer with World Ease. The service levels are as follows:

S	UPS Standard\
V	UPS Express Saver\
P	UPS Express Plus\
N	UPS Express NA1\
R	UPS Express\
D	UPS Expedited\
The 'ServiceLevel' column in the POE file can also list combinations of service levels, e.g.

RV --> UPS Express and UPS Express Saver are allowed within one World Ease shipment\
RPV --> UPS Express, UPS Epress Plus and UPS Express Saver are allowed within one World Ease shipment\
Documents\
The documents needed for World Ease see below

Possible variants for World Ease shipments\
Variant 1: UPS World Ease – with DocBox\
Master-shipment contains shipment documents.

Master-shipment specification:\
1 package with dimensions L/W/H each 1 cm, weight 1 kg must be created. Set UPS "02 - customer's own packaging" for package conversion\
this package represents the green document box containing the transport documents for World Ease shipments\
A label is printed for each package in the child-shipment and for the package in the master-shipment\
For the master-shipment, the MasterInvoice document and the CID are also printed.\
Please note "Trade document upload" not possible with this variant!

Variant 2: UPS World Ease – Paperless Invoice with DocBox\
Master-shipment with Paperless Invoice and shipment documents.

Master shipment specification:\
1 package with dimensions L/W/H 1 cm each, weight 1 kg must be created\
this package represents the green document box containing the transport documents for World Ease shipments\
Child-shipment specification:\
Paperless Invoice (additional documents) must be activated in each child shipment\
A label is printed for each package in the child-shipment and for the package in the master-shipment\
For the master-shipment the document MasterInvoice and the CID will be printed additionally\
Variant 3: UPS World Ease – Paperless Invoice without DocBox\
Master shipment with Paperless Invoice without shipment documents.

Master-Shipment specification:\
There is no package, a virtual package is generated in the shipment\
Child shipment specification:\
Paperless Invoice must be activated in each child shipment\
A label is printed for each package in the child-shipment\
For the master-shipment the SummaryLabel is printed, which should be stuck on the last package\
Neither MasterInvoice nor CID are printed for the master-shipment.

**Return services**

With the "Return Service - Electronic Return Label (Label Sent by UPS via Email)" the customer transfers us a data record (PLD0200, XML APIs, WorldShip, but also Internet Shipping) electronically, UPS generates on its own servers a shipping label which is sent to the end customer by email for self-printing. Therefore, in this case, the e-mail address of the collection customer is mandatory.\
"Return service - Print Return label (self printing)": In the variant with the printout of a label, which the customer sends to the receiver via PDF, we rather speak of "return service self-printing".\
All three variants have in common that UPS does not proactively drive to the customer to pick up a provided package but waits for the customer to contact us. UPS then reactively sends a driver to pick up the package.

The following value added return services are implemented for UPS in CCO:

Return Service – Electronic Return Label\
You have the option to provide your customers in over 135 countries with a return shipping label via email. Your customer can print this label and the control document or drop off the package at an authorized UPS shipping location before contacting UPS to arrange a pickup.

As soon as a corresponding EDI has been transmitted to UPS, UPS generates a shipping label on its own servers which is sent to the collection customer by e-mail for self-printing. Therefore, in this case, the e-mail address of the collection customer is mandatory, i.e. to fill in CCO.\
Return Service – Print Return Label\
With the "Return Service - Print Return Label (Self print)", you can print the return label yourself and include it with outgoing shipments to over 135 countries. You can also send the label separately to your customer after shipping the package separately. Customers then simply affix the label to their package or drop off the package at an authorized UPS shipping location and contact UPS for a pickup.

when transferring to CCO, the user gets back a label, which he then saves e.g. via PDF print in a directory or manually attaches to an email\
Return Service – One Attempt\
With this service you can order a pickup for immediate return of a package. The UPS driver will make an attempt to pick up the package. If the driver does not meet the customer at the "UPS Return Service - One Attempt", he leaves the sticker with the customer, who then simply affixes it to the package and either takes it to a UPS drop-off point or contacts UPS for collection.

no label is generated during the transfer to CCO. The EDI transfer counts as an order for UPS. The UPS driver brings a label to the customer and attaches it to the package there.\
Return Service – Three Attempt\
With this service you can order a pickup for immediate return of a package. The UPS driver will make three attempts to pick up your shipment on three consecutive business days. If the driver still cannot pick up the shipment on the third attempt, the label will be returned to UPS.

no label is generated during the transfer to CCO. The EDI transmission counts as an assignment for UPS. The UPS driver brings a label to the customer and attaches it to the package there.\
Return Service - Print & Mail - invalid as of FP 08/2022
