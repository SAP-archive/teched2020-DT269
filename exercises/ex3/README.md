# Exercise 3 - Interaction between ITCM and Kyma runtime

Now, let's start the interaction!
First, sync a claim in ITCM. ITCM publishes the "Claim Created" event through the channel predefined in ITCM Extension Center.
Function *itcm-func-exec* do the event persistence. 
The mobile app syncs the event data by calling function *itcm-func-fetch*.
From the mobile app, a retailer process an event by taking a pic of an invoice document.
Function *itcm-func-upload* process the pic, call a 3rd party OCR service by REST API. 
Extract a remark, update related claim with an extracted remark, and the invoice document as an attachment.

## Step 3.1 - Sync a new claim which has an empty remark in ITCM

Sync to show a new incoming claim with an empty remark and no attachment. 

Press the sync button on the ITCM list view, take newly created claim 5600 as an example.
<br>![](/exercises/ex3/images/e3-itcm-claim-created.png)

Empty remark for claim 5600.
<br>![](/exercises/ex3/images/e3-itcm-claim-detail.png)

Empty attachment for claim 5600.
<br>![](/exercises/ex3/images/e3-itcm-claim-empty-attachment.png)

## Step 3.2 - Upload invoice pic to Kyma runtime from the ITCM mobile app

From a retailer's mobile app, scroll down to claim 5600, process the claim by taking a pic of an invoice document.

Find claim 5600 from the retailer mobile app.
<br>![](/exercises/ex3/images/e3-mobile-process-event.png)

Take a pic of an invoice document for claim 5600.
<br>![](/exercises/ex3/images/e3-mobile-upload-invoice.png)

## Step 3.3 - Upload function process the invoice pic in Kyma runtime and update claim in ITCM

Go back to claim 5600 detail in ITCM, remark filled.
<br>![](/exercises/ex3/images/e3-itcm-remark.png)

Also, the attachment file was uploaded.
<br>![](/exercises/ex3/images/e3-itcm-claim-attachment.png)

## Summary

You've now completed the Exercise and learned

- Pair ITCM & Kyma runtime.
- Implement an extensional service by creating a serverless function in Kyma runtime.
- Powerful Extensibility ITCM provided, demonstrated by an e2e user case.

