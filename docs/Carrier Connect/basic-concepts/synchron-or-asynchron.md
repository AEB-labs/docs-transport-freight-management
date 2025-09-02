---
title: Synchronous or asynchronous
excerpt: 'ProcessParms: Choosing the right "Processing Mode"'
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: noindex
next:
  description: ''
  pages:
    - type: basic
      slug: printing-documents
      title: Printing documents
---
## Processing mode

API calls can be performed synchronously or asynchronously.

These options are provided to match the shipping context and the technical capabilities of the calling system.\
*Synchronous* communication responds with more distinct results. No additional lookup to verify the final result of an operation is needed. On the other hand, it closely links the calling system with Carrier Connect and sometimes it might be preferable to avoid this.\
In the *asynchronous* communication mode, Carrier Connect checks whether it is generally possible to perform an operation (e.g. check transactionId for uniqueness) and accepts the task if no issues are detected. Only then, more sophisticated validations are performed. The calling system only learns about possible warnings by frequently synchronizing with Carrier Connect using the sync calls of the API.

**Process mode "BASIC"**\
Triggers asynchronous communication. Default mode if nothing else is provided.\
The operation is processed in an asynchronous job after performing some basic checks.

```json
"processParms": {
    "processMode": {
      "mode": "BASIC"
    },
...
```
```xml
<processParms>
     <processMode>
         <mode>BASIC</mode>
     </processMode>
     ...
</processParms>
```

**Process mode "EXTENDED"**\
Triggers synchronous communication.\
The operation is executed directly within the API request transaction and no response is returned until the process is finished.

```json
"processParms": {
    "processMode": {
      "mode": "EXTENDED"
    },
...
```
```xml
<processParms>
     <processMode>
         <mode>EXTENDED</mode>
     </processMode>
     ...
</processParms>
```
