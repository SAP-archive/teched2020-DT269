# Introduction

The demo is an e2e integrated case that presents ITCM extensibility from Kyma runtime.

Business Story:

**From ITCM**,</br>
New claim sync in ITCM publish a claim created domain event, which is subscribed by a serverless function in Kyma runtime, persists event, and prepares for the processing later on.

**From a retailer mobile App**,</br>
events show as notifications by calling rest API exposed by another serverless function in Kyma runtime.</br>
Process the new notification, take a pic of an invoice document. The pic will be uploaded to a third serverless function in Kyma runtime, which will process the pic, call a third party OCR service, generate remark and update the related claim record in ITCM directly.

## Architecture

ITCM follows an event-driven architecture.
With a pub-sub pattern, ITCM publishes events to Kyma runtime through a predefined channel, then
serverless functions subscribed related channels in Kyma runtime will handle the events. 

### Architecture Diagram

![](/exercises/ex0/images/kyma-integration-demo-architecture-diagram.png)

## Scenario Diagram

Two operating lines for this case:
- A tenant's claim syncing will kick off the process. ITCM send Claim Created event to Kyma runtime.
- A retailer from a mobile app handles the event by taking a pic of an invoice document.

![](/exercises/ex0/images/kyma-integration-demo-diagram.png)

## Summary

Start exercise - [Exercise 1 - Setup connection between ITCM and Kyma runtime](../ex1/README.md)
