# DT269 - Extensibility for SAP Intelligent Trade Claims Management(ITCM) from project Kyma

This repository contains the material for the SAP TechEd 2020 session called DT269 - Extensibility for SAP Intelligent Trade Claims Management(ITCM) from the project Kyma.  

## Overview

This session introduces attendees to SAP ITCM extensibility from Kyma runtime, which brings smooth integration experiences between ITCM and Kyma runtime. 
The extensibility not only makes possible integration between ITCM and SAP on promise solution via Kyma runtime but also can be leveraged by partners to provide customized solutions and full fill their e2e user cases around ITCM.

- **ITCM** </br>
A Kubernetes based SaaS offering, behind the scenes, is composed of serval micro-services. Communication with each other is mostly events, which is known as an event-driving architecture.

- **Kyma runtime**

> Kyma is a cloud-native extensibility framework developed to overcome the challenges of digital transformation, which include heterogeneous product portfolio, monolithic deployments, and cloud-native development. Our goal is to provide application extensions in a cloud-native fashion and with increased agility through seamless integration with the products.</br>
 \- cxwiki.sap.com

ITCM build-in supports for Kyma runtime, in ITCM Extension Center, users can easily register Kyma runtime, publish Event Mesh or Open API to Kyma runtime. 
Use a serverless function for a customized solution in Kyma runtime. With a serverless function, partners can focus on the integration logic only. 
CI/CD part like building, deployment, autoscaling, etc., will be taken over by Kyma runtime.

The exercises demonstrate an e2e integration case from ITCM to Kyma step by step.

## Requirements

- ITCM solution provisioned on cloud
- Kyma runtime provisioned by SAP Cloud Platform(SCP) or Kyma cli on cloud

## Exercises

- [Introduction](exercises/ex0/)
    - [Architecture](exercises/ex0#architecture)
    - [Demo Scenario](exercises/ex0#scenario-diagram)
- [Exercise 1 - Setup connection between ITCM and Kyma runtime](exercises/ex1#exercise-1---setup-connection-between-itcm-and-kyma-runtime)
    - [Step 1.1 - Create ITCM application in Kyma runtime](exercises/ex1#step-11---create-an-itcm-application-in-kyma-runtime)
    - [Step 1.2 - Register Kyma runtime in ITCM Extension Center](exercises/ex1#step-12---register-kyma-runtime-in-itcm-extension-center)
    - [Step 1.3 - Register ITCM exposed domain event APIs](exercises/ex1#step-13---register-itcm-exposed-domain-event-apis)
- [Exercise 2 - Implement extensional functions in Kyma runtime](exercises/ex2/)
    - [Step 2.1 - Create an exec function for consuming ITCM domain events](exercises/ex2#step-21---create-an-exec-function-for-consuming-itcm-domain-events)
    - [Step 2.2 - Create a fetch function, expose API for the external solution](exercises/ex2#step-22---create-a-fetch-function-expose-api-for-the-external-solution)
    - [Step 2.3 - Create an upload function, process ITCM domain event](exercises/ex2#step-23---create-an-upload-function-process-itcm-domain-event)
- [Exercise 3 - Interaction between ITCM and Kyma runtime](exercises/ex3/)
    - [Step 3.1 - Sync a new claim which has an empty remark in ITCM](exercises/ex3#step-31---sync-a-new-claim-which-has-an-empty-remark-in-itcm)
    - [Step 3.2 - Upload invoice pic to Kyma runtime from the ITCM mobile app](exercises/ex3#step-32---upload-invoice-pic-to-kyma-runtime-from-the-itcm-mobile-app)
    - [Step 3.3 - Upload function process the invoice pic in Kyma runtime and update claim in ITCM](exercises/ex3#step-33---upload-function-process-the-invoice-pic-in-kyma-runtime-and-update-claim-in-itcm)

Exercises demo video [here](https://sap.sharepoint.com/:v:/r/teams/S4HANALabs-Eureka/Shared%20Documents/04%20-%20Engineering%20%26%20Ops/Tech%20Foundations/teched/TechEd.mp4?csf=1&web=1&e=Ll7Q6V).

**IMPORTANT**

Your repo must contain the .reuse and LICENSES folder and the License section below. DO NOT REMOVE the section or folders/files. Also, remove all unused template assets(images, folders, etc) from the exercises folder. 

## How to obtain support

Support for the content in this repository is available during the actual time of the online session for which this content has been designed. Otherwise, you may request support via the [Issues](../../issues) tab.

## License

Copyright (c) 2020 SAP SE or an SAP affiliate company. All rights reserved. This file is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSES/Apache-2.0.txt) file.
