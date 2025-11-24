---
title: Copy of [Carrier Name] Account Configuration
deprecated: false
hidden: true
metadata:
  robots: index
---
<CCOConfiguringCarriersInCarrierConnect />

To create a new DSV Air Freight (Europe) account in Carrier Connect, open DSV Air Freight (Europe) in *Master data > Carrier configurations*. In the tab *Accounts* click on *New*. Select account type DSVAIR_API2 (standard to be used). The type DSVAIR_APITRACK2 is deprecated.

# DSV Air Freight (Europe) account

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
    <tr>
      <td>1</td>
      <td>Shipper</td>
      <td>The address of the shipper</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Carrier address</td>
      <td>The address of the carrier (depot)</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Condition</td>
      <td>See our <Anchor label="user guide" target="_blank" href="https://docs.aeb.com/doc/cm-620065803-801708043-de-DE/t-801708043-709043211-de-DE">user guide</Anchor></td>
    </tr>
    <tr>
      <td>4</td>
      <td>Single pkg. handling</td>
      <td>See <a href="https://transport-freight-management.docs.developers.aeb.com/docs/dhlfreight-account-configuration#single-package-handling">Single Package Handling</a></td>
    </tr>
    <tr>
      <td>5</td>
      <td>Package no. range</td>
      <td>See <a href="https://transport-freight-management.docs.developers.aeb.com/docs/copy-of-ups-emea-carrier-configuration#package-number-range">Package number range</a></td>
    </tr>
    <tr>
      <td>6</td>
      <td>EDI transmission</td>
      <td>Set to <em>Send and log</em></td>
    </tr>
    <tr>
      <td>7</td>
      <td>Customer no.</td>
      <td>Assigned by the carrier</td>
    </tr>
    <tr>
      <td>8</td>
      <td>GS1 base no.</td>
      <td>Your company's GS1 base number</td>
    </tr>
    <tr>
      <td>9</td>
      <td>Package no. range</td>
      <td>Assigned by the carrier</td>
    </tr>
    <tr>
      <td>10</td>
      <td>Test user name</td>
      <td>Assigned by the carrier</td>
    </tr>
    <tr>
      <td>11</td>
      <td>Test password</td>
      <td>Assigned by the carrier</td>
    </tr>
    <tr>
      <td>12</td>
      <td>Test subscription key (Web service data)</td>
      <td>Assigned by the carrier</td>
    </tr>
    <tr>
      <td>13</td>
      <td>Test subscription key (Document upload)</td>
      <td>Assigned by the carrier</td>
    </tr>
    <tr>
      <td>14</td>
      <td>Test auth sub. key</td>
      <td>Assigned by the carrier</td>
    </tr>
  </tbody>
</Table>

<CCOSinglePackageHandling />

<br />

<CCOPackageNumberRange />

<br />

| Number | Field          | Comment                                                                       |
| :----- | :------------- | :---------------------------------------------------------------------------- |
| 1      | Abbreviation   | Choose a descriptive abbreviation. E.g. DSV Air Freight (Europe)_PCK          |
| 2      | Name           | Choose a descriptive name. E.g. DSV Air Freight (Europe) package number range |
| 3      | Start value    | *Ask the user for this value*                                                 |
| 4      | Max. value     | *Ask the user for this value*                                                 |
| 5      | Auto. re-start | Activated or Deactivated                                                      |
| 6      | Leading zeros  | Activated or Deactivated                                                      |
| 7      | Char. length   | *Ask the user for this value*                                                 |
