---
title: Understanding Customer Account Numbers
excerpt: >-
  This paragraph describes how Carrier Connect utilizes customer account numbers
  (in processing freight costs and duties).
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
<HTMLBlock>{`
<style>
  span.cm-s-neo {
    background-color: #f2f2f2;
    color: red;
  }
</style>
`}</HTMLBlock>

> 📘 What's a customer account number?
>
> A customer account number is a unique identifier assigned to an individual or business entity by the carrier to identify them as a customer. When a carrier wants to bill something to a party, they typically require the party's customer account number to ensure accurate and timely billing.

The *term of delivery* of a <Glossary>shipping order</Glossary> outlines who pays for the freight costs and, in the case of exports, who pays duties and taxes.

![](https://files.readme.io/732aa17-image.png)Options for **freight costs**

* **Free**: The shipper (the party sending the goods) pays.
* **Chargeable**: The consignee (the party receiving the goods) or a third party pays.

Options for **duties and taxes**

* **Duty paid / taxed**: The shipper pays.
* **Duty unpaid / untaxed**: The consignee or a third party pays.

> 📘 Mandatory fields
>
> The freight costs are always mandatory, as every shipment requires an incoterm and the payer of freight always has to be defined.
>
> The payer of duty is only needed if the shipment is dutiable, it should not be filled if duties are not applicable (e.g. a domestic shipment, or a shipment within the European Union).

To correctly bill the appropriate party, the carriers require the account number of that party.

## Shipper's Customer account number

This is stored in the carrier master data/account of the carrier configuration. You can set up several accounts within one carrier (e.g. if there are branches, each can be represented with a unique account number within the carrier). As soon as the number of accounts is more than 1, conditions for each account must be maintained to ensure the right selection. The account determination takes place when importing a shipping order to Carrier Connect. To learn more about how to configure account conditions, have a look at our [configuration guide](https://docs.aeb.com/doc/cm-620065803-801708043-en-US/t-801708043-709043211-en-US).

## Customer account number of freight payer and/or debtor

Defines which account the carrier charges freight or customs duties to. There are two options:

1. If the **sender** pays the freight or customs duties, Carrier Connect uses the account number stored in the carrier master data in the account (see above).

   ```json
   "shipment": {
     ...
     // The payer of freight charges
     "payerOfChargRole": "SHIPPER",
     ...
     // The payer of duties and taxes
     "payerOfDutRole": "SHIPPER",
   }
   ```
   ```xml
   <shipment>
     <!-- The payer of freight charges -->
     <payerOfChargRole>SHIPPER</payerOfChargRole>
     <!-- The payer of duties and taxes -->
     <payerOfDutRole>SHIPPER</payerOfDutRole>
   </shipment>
   ```

   > 🚧 Required data
   >
   > If you're using SHIPPER, don't transmit the **address data** (`payerOfCharg` or `payerOfDut`) and the **account number** (`payerOfChargAccountNo` or `payerOfDutAccountNo`) since this data is already available in the Carrier Connect master data.
2. If the **Consignee** or a **Third Party** pays the freight/duties, that party's account number is required. 

   ```json
   "shipment": {
     ...
     // The payer of freight charges
     "payerOfChargRole": "RECEIVER",
     ...
     // The payer of duties and taxes
     "payerOfDutRole": "THIRDPARTY",
   }
   ```
   ```xml
   <shipment>
     <!-- The payer of freight charges -->
     <payerOfChargRole>RECEIVER</payerOfChargRole>
     <!-- The payer of duties and taxes -->
     <payerOfDutRole>THIRDPARTY</payerOfDutRole>
   </shipment>
   ```

   > 🚧 Required data
   >
   > If you're using RECEIVER, don't transmit the **address data** (`payerOfCharg` or `payerOfDut`) since you already transmitted this data in the consignee address segment.

   There are two ways to fill this **account number** in the specific shipping order:

   1. Via the interface: `payerOfChargAccountNo` / `payerOfDutAccountNo` plus, if applicable, the address segment (e.g. `payerOfDut`).
      ```json
      "shipment": {
        ...
        // The payer of charges account number
        "payerOfChargAccountNo": "1234567"
        ...
        // The payer of duties and taxes account number
        "payerOfDutAccountNo": "1234567",
      }
      ```
      ```xml
      <shipment>
        <!-- The payer of charges account number -->
        <payerOfChargAccountNo>1234567</payerOfChargAccountNo>
        <!-- The payer of duties and taxes account number -->
        <payerOfDutAccountNo>1234567</payerOfDutAccountNo>
      </shipment>
      ```
   2. Via the company master data from CCO: `initPayerOfChargAccNoFromCompanyMasterData` / `initPayerOfDutAccNoFromCompanyMasterData` must be `true` in this case. The name of the freight payer/customs debtor (e.g. `payerOfDut.name`) must then be entered in the interface so that matching with the CCO master data can take place.

      ```json
      "shipment": {
        ...
        // If true, the account number will be filled with the appropriate number in the company master
        // data referenced by the 'payerOfCharg.name' field or (if filled) 
        // 'payerOfCharg.companyNumber' field.
        "initPayerOfChargAccNoFromCompanyMasterData": true
        ...
        // f true, the account number will be filled with the appropriate number in the company master 
        // data referenced by the 'payerOfDut.name' field or (if filled) the 
        // 'payerOfDut.companyNumber' field.
        "initPayerOfDutAccNoFromCompanyMasterData": true,
      }
      ```
      ```xml
      <shipment>
        <!-- If true, the account number will be filled with the appropriate number in the company master data referenced by the 'payerOfCharg.name' field or (if filled) 'payerOfCharg.companyNumber' field. -->
        <initPayerOfChargAccNoFromCompanyMasterData>true</initPayerOfChargAccNoFromCompanyMasterData>
        <!-- If true, the account number will be filled with the appropriate number in the company master data referenced by the 'payerOfDut.name' field or (if filled) the 'payerOfDut.companyNumber' field. -->
        <initPayerOfDutAccNoFromCompanyMasterData>true</initPayerOfDutAccNoFromCompanyMasterData>
      </shipment>

      ```

<HTMLBlock>{`
<style>
  details {
    background-color: #FDF7F7;
    padding: 10px;
    margin-left: 90px;
    border-left: 3px solid #D9534F;
    /* border-radius: 5px; */
  }
</style>

<details>
  <summary>Click for more info on: How to Configure an Account Number in the Company Master Data</summary>
  <iframe src="https://scribehow.com/embed/How_to_Configure_an_Account_Number_in_the_Company_Master_Data__18KwHeTlRlyX6q9Mbdt6Sw" width="100%" height="640" allowfullscreen frameborder="0"></iframe>
</details>
`}</HTMLBlock>
