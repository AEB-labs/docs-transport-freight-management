---
title: Handling company data in Carrier Connect
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Firmendaten an CCO übertragen

## Alle Daten in der API übergeben

```
"shippingPt": {
      "city": "Hamburg",
      "companyNumber": "001-2",
      "countryISOCode": "DE",
      "name": "Versand GmbH",
      "postcode": "20457",
      "street": "Speicherstadt 1"
    },
```

## Firmendaten aus CCO Stammdaten initialisieren

```
"shippingPt": {
      "companyNumber": "001-2",
      "name": "Versand GmbH",
      "initFromCompanyMasterFileData": true
         },
```

# Firmendaten als Stammdaten importieren

## CSV

## API

`setCompanyMasterFileData`

```xml
<clientSystemId>SOAP</clientSystemId>
<clientIdentCode>CLIENT</clientIdentCode>
            <userName>WSM</userName>
            <resultLanguageIsoCodes>DE</resultLanguageIsoCodes>
            <companies>
               <companyNumber>1234</companyNumber>
               <companyExtensions>
                  <extensionDataType>?</extensionDataType>
               </companyExtensions>
               <name>TestFirma</name>
               <street>Street 1</street>
               <postcode>70567</postcode>
               <city>Stadt</city>
               <countryISOCode>DE</countryISOCode>
            </companies>
```

<br />

- ["Doku"](https://rz3.aeb.de/test1cai/servlet/bf/doc/LogisticsBF/de/aeb/xnsg/logistics/bf/ILogisticsBF.html#setCompanyMasterFileData(de.aeb.xnsg.logistics.bf.SetCompanyMasterFileDataRequestDTO))
- <https://rz3.aeb.de/test1cai/servlet/bf/doc/LogisticsBF/de/aeb/xnsg/logistics/bf/ILogisticsBF.html>