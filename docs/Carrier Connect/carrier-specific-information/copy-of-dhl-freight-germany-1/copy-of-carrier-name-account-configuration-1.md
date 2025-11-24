---
title: Copy of [Carrier Name] Account Configuration
deprecated: false
hidden: true
metadata:
  robots: index
---
<CCOConfiguringCarriersInCarrierConnect />

To create a new DSV Air Freight (Europa) account in Carrier Connect, open DSV Air Freight (Europa) in *Master data > Carrier configurations*. In the tab *Accounts* click on *New*.

When prompted to select an account type, choose **DSVAIR_API2 (DSV Luftfracht API Standard-Acc...)**. Do not use the deprecated **DSVAIR_APITRACK2** type.

# DSV Air Freight (Europa) account

<Image align="center" border={false} src="" />
<Image align="center" border={false} src="" />

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>Number</th>
      <th>Field</th>
      <th>Comment</th>
    </tr>
  </thead>
  <tbody>
    {/* Predefined fields */}
    <tr>
      <td></td>
      <td>Shipper</td>
      <td>The address of the shipper.</td>
    </tr>
    <tr>
      <td></td>
      <td>Carrier address</td>
      <td>The address of the carrier (depot).</td>
    </tr>
    <tr>
      <td></td>
      <td>Condition</td>
      <td>See our <Anchor label="user guide" target="_blank" href="https://docs.aeb.com/doc/cm-620065803-801708043-de-DE/t-801708043-709043211-de-DE">user guide</Anchor>.</td>
    </tr>
    <tr>
      <td></td>
      <td>Single pkg. handling</td>
      <td>See <Anchor label="Single Package Handling" target="_blank" href="https://transport-freight-management.docs.developers.aeb.com/docs/dhlfreight-account-configuration#single-package-handling">Single Package Handling</Anchor>.</td>
    </tr>
    <tr>
      <td></td>
      <td>Package no. range</td>
      <td>Select the number range used to generate package numbers for this account. See <Anchor label="Package number range" target="_blank" href="https://transport-freight-management.docs.developers.aeb.com/docs/copy-of-ups-emea-carrier-configuration#package-number-range">Package number range</Anchor>.</td>
    </tr>
    <tr>
      <td></td>
      <td>EDI transmission</td>
      <td>Set to <i>Send and log</i>.</td>
    </tr>

{/* Screenshot-extracted fields */}
<tr>
  <td>1</td>
  <td>DSVAIR_API2 (DSV Luftfracht API Standard-Acc...)</td>
  <td>Select this type in the account type dialog. This is the standard and required account type; the DSVAIR_APITRACK2 type is deprecated and must not be used.</td>
</tr>
<tr>
  <td>2</td>
  <td>Customer no.</td>
  <td>Enter the customer number assigned by DSV for this air freight account.</td>
</tr>
<tr>
  <td>3</td>
  <td>GS1 base no.</td>
  <td>Enter the GS1 company prefix to be used for label and package number generation with DSV.</td>
</tr>
<tr>
  <td>4</td>
  <td>Test user name</td>
  <td>Enter the username for the DSV API test environment.</td>
</tr>
<tr>
  <td>5</td>
  <td>Test password</td>
  <td>Enter the password for the DSV API test environment corresponding to the test user name.</td>
</tr>
<tr>
  <td>6</td>
  <td>Test subscription key</td>
  <td>In section <i>Web service data</i>, enter the subscription key for accessing the DSV air freight API in the test environment.</td>
</tr>
<tr>
  <td>7</td>
  <td>Test subscription key</td>
  <td>In section <i>Document upload</i>, enter the subscription key for the DSV document upload service in the test environment.</td>
</tr>
<tr>
  <td>8</td>
  <td>Test auth sub. key</td>
  <td>Enter the authentication subscription key for the DSV test environment in section <i>Authentication</i>.</td>
</tr>

  </tbody>
</Table>

<CCOSinglePackageHandling />

<br />

<CCOPackageNumberRange />

<br />