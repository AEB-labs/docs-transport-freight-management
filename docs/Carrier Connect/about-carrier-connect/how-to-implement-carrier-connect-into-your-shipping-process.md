---
title: Integration Overview
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
In this **Getting Started** section you'll get to know 

When integrating Carrier Connect into your host system, the following two steps are required: 

# 1. API Configuration & Field Mapping

Before the API can be used effectively, the data structures of the host system and the carrier system must be aligned. This step involves:

Mapping the relevant fields from the host system to the corresponding API fields.  
Understanding and configuring control fields that influence API behavior (e.g., shipment types, service levels, packaging specifications).  
Ensuring proper data transformation where required (e.g., converting date formats, adjusting weight units).  
Proper API Configuration & Field Mapping is essential for accurate data exchange, preventing errors, and ensuring the carrier system correctly interprets the provided information.

# 2. Process Integration

Once the data is properly mapped, the next step is integrating API calls into the customer’s shipment workflow. This involves:

Defining how shipments are processed within the customer’s system and identifying which API interactions are needed at each step.  
Embedding API calls (e.g., shipment creation, updates, cancellations) into the host system’s operational processes.

- Handling API responses and errors to ensure smooth automation and user experience.  
  How These Steps Work Together  
  The two steps are closely interconnected: the specific API calls required are determined by the shipment process of the customer. Different workflows may necessitate different API calls or sequences—for example, some processes might require shipment updates before label printing, while others might cancel shipments under specific conditions.

This means that Process Integration defines which API calls are needed, and API Configuration & Field Mapping ensures those calls are correctly implemented. A well-executed integration enables efficient shipment processing, real-time tracking, and accurate label printing, ultimately improving operational efficiency and customer satisfaction.