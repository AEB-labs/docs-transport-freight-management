---
title: 'UPS EMEA: General Information'
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# General Information

## UPS Certification - UPS Ready Vendor

The UPS Ready Vendor Certification is a program by United Parcel Service (UPS) that recognizes third-party software providers that integrate UPS shipping, tracking, and logistics solutions into their products. This certification ensures that the vendor's software meets UPS’s standards for seamless integration and reliable performance.

> 📘 AEB is UPS Ready Vendor
> 
> **To facilitate a simplified acceptance process, please provide the following information to your UPS contact person:**

| Software Name | Software-Version | Software Vendor Code |
| :------------ | :--------------- | :------------------- |
| CCO           | 985.A.000        | 985                  |

## Time of data transmission

### Shipping data

<CCOShippingDataViaEDI />

The UPS format is called PLD200.

### Document upload

Documents will be uploaded when closing the <<glossary:pickup>>.

### Webservice for Dangerous Goods, Access Points or Trade document upload

<CCOUPSWebservice />

# Acceptance Process

At the beginning of the implementation, AEB will provide you with a digital questionnaire that will ask for all the information required to connect to UPS. You will then use this information to configure UPS in Carrier Connect. Details on how to configure Carrier Connect can be found here: [UPS Carrier Configuration](doc:carrier-configuration).

Once UPS is fully configured, you can begin the acceptance process. To do this, you will create the required test shipments and generate labels and EDI, which will then be reviewed by UPS. You will receive the exact acceptance requirements from your UPS contact. 

Once you receive acceptance from UPS, we will transfer the carrier configuration to the production system so you can use it productively.