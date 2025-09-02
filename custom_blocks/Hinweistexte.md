---
name: Hinweistexte
---
# Info texts

<Callout icon="💡" theme="default">
  ### German: Hinweistexte
</Callout>

![](https://files.readme.io/f6cf6c1-image.png)

Info texts are used by carriers that need or can process additional data of a specific text type. 

The type of available info texts varies for each carrier. The available info texts can be found in the specific carrier section of the <a href="https://rz3.aeb.de/docudata/system-descriptions/carrier-connect/sd-carrierconnect-carrieroverview/en-US/index.html#index_content" target="_blank">System Description</a> of Carrier Connect. If the info texts section does not exist, the carrier does not have specific info texts, or does not have any info texts other than the reference texts.  

```json

"shipment": {
  "carrierInfoTexts": [
    {
      "identCode": "003",
      "parameter": "81685818"
    }
  ],
  ...
}
  
```
```xml
<shipment>
  <carrierInfoTexts>
      <identCode>003</identCode>
      <parameter>81685818</parameter>
  </carrierInfoTexts>
  ...
</shipment>
```

To use the info texts there are two fields to be filled:

* `identCode`: Code of the info text field - see abbreviation in front of the name in the <a href="https://rz3.aeb.de/docudata/system-descriptions/carrier-connect/sd-carrierconnect-carrieroverview/en-US/index.html#index_content" target="_blank">System Description</a> of Carrier Connect.  
* `parameter`: Value of the info text field.

![](https://files.readme.io/17a9b37-image.png)
