---
title: Synchronizing settlements and external invoices
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
Logistics Cost Management provides APIs to track changes of settlements and external invoices. These APIs allow partner systems to fetch data about changes that happened in Logistics Cost Management. 

> 📘 Typical use cases for synchronization
> 
> - Trace progress of invoice audit or settlement process.
> - React to status milestones of settlements and external invoices.

# How to synchronize settlements?

> 💡 Enable tracking of changed settlements
> 
> Before synchronization, tracking of changes must be set up within Logistics Cost Management.

1. Request changed settlements
   - Partner system calls [getChangedSettlements ](https://transport-freight-management.docs.developers.aeb.com/reference/getchangedsettlements).
   - The return contains a list of up to 100 objects that were changed since the last synchronization.
   - The return also contains a flag `isComplete` that indicates whether there are further objects that need to be synchronized. This flag is relevant for step 3.
2. Process changed settlements and acknowledge recieve.
   - The partner system processes the objects and calls [acknowledgeChangedSettlements](https://transport-freight-management.docs.developers.aeb.com/reference/acknowledgechangedsettlements).
   - The objects are now marked as "synchronized" in Logistics Cost Management.
   - If the partner system could not process the objects successfully it should not call `acknowledgeChangedSettlements`. The next call to `getChangedSettlements` will then return the same objects as before.
3. Repeat if synchronization is not complete
   - If there are more changed objects to synchronize go back to step 1.

# How to synchronize external invoices?

External invoices are synchronized analogously to the procedure above by using [getChangedExternalInvoices](https://transport-freight-management.docs.developers.aeb.com/reference/getchangedexternalinvoices) and [acknowledgeExternalInvoice](https://transport-freight-management.docs.developers.aeb.com/reference/acknowledgechangedexternalinvoices).