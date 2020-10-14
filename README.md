# DT269 - Extensibility for SAP Intelligent Trand Claims Management(ITCM) from project "Kyma"

This repository contains the material for the SAP TechEd 2020 session called DT269 - Extensibility for SAP Intelligent Trand Claims Management(ITCM) from project "Kyma".  

## Overview

This session introduces attendees to SAP ITCM extensibility from Kyma runtime, which brings smooth integration experiences between ITCM and Kyma runtime. The extensibility not only makes possible integration between ITCM and SAP on promise solution via Kyma runtime but also can be leveraged by partners to provide customized solution and full fill their e2e user cases around ITCM.

- **ITCM**<br>
A Kubernetes base SaaS offering, behind the scences is composed by serval micrio-services. The conmunicate with each other are mostly event, which is known as an event-driving architecture.

- **Kyma runtime**
> Kyma is a cloud-native extensibility framework developed to overcome the challenges of digital transformation, which include heterogeneous product portfolio, monolithic deployments and cloud native development. Our goal is to provide application extensions in a cloud-native fashion and with increased agility through seamless integration with the products.<br>
 \- cxwiki.sap.com

ITCM build-in supports for Kyma runtime, in ITCM Extension Center, user can easily register Kyma runtime, publish event Mesh or Open API to Kyma runtime. Customized solution can be implemented as a serverless function in Kyma runtime. In a serverless fasion, partners can focus on the integration code only, the CI/CD part like building, deployment, autoscale, etc, will be taken over by Kyma runtime. 

The 3 exercises demonstrate an e2e integration case from ITCM to Kyma step by step.

## Requirements

- ITCM solution provisioned on cloud
- Kyma runtime provisioned by Gardener or SAP Cloud Platform(SCP) on cloud

## Exercises

- [Introduction](exercises/ex0/)
    - [Architecture](exercises/ex1#exercise-11-sub-exercise-1-description)
    - [Demo Scenario](exercises/ex1#exercise-11-sub-exercise-1-description)
- [Exercise 1 - Setup connection between ITCM and Kyma runtime](exercises/ex1/)
    - [Step 1.1 - Register Kyma runtime in ITCM Extension Center](exercises/ex1#exercise-11-sub-exercise-1-description)
    - [Step 1.2 - Create ITCM application in Kyma runtime](exercises/ex1#exercise-12-sub-exercise-2-description)
    - [Step 1.3 - Register ITCM exposed domain event APIs on Kyma runtime](exercises/ex1#exercise-12-sub-exercise-2-description)
- [Exercise 2 - Implement extensional functions in Kyma runtime](exercises/ex2/)
    - [Step 2.1 - Create an exec function for consuming ITCM domain events in Kyma runtime](exercises/ex2#exercise-21-sub-exercise-1-description)
    - [Step 2.2 - Create a fetch function, expose API for the external solution in Kyma runtime](exercises/ex2#exercise-21-sub-exercise-1-description)
    - [Step 2.3 - Create an upload function, process ITCM domain event in Kyma runtime](exercises/ex2#exercise-21-sub-exercise-1-description)
- [Exercise 3 - Interaction between ICTM and Kyma runtime](exercises/ex2/)
    - [Step 3.1 - Sync a new claim which has an empty remark in ITCM](exercises/ex2#exercise-21-sub-exercise-1-description)
    - [Step 3.2 - Upload invoice pic to Kyma runtime from the ITCM mobile app](exercises/ex2#exercise-22-sub-exercise-2-description)
    - [Step 3.3 - Upload function process the invoice pic in Kyma runtime and update claim in ITCM](exercises/ex2#exercise-22-sub-exercise-2-description)

exercises demo video [here](https://sap.sharepoint.com/:v:/r/teams/S4HANALabs-Eureka/Shared%20Documents/04%20-%20Engineering%20%26%20Ops/Tech%20Foundations/teched/TechEd.mp4?csf=1&web=1&e=Ll7Q6V).

**IMPORTANT**

Your repo must contain the .reuse and LICENSES folder and the License section below. DO NOT REMOVE the section or folders/files. Also, remove all unused template assets(images, folders, etc) from the exercises folder. 

## How to obtain support

Support for the content in this repository is available during the actual time of the online session for which this content has been designed. Otherwise, you may request support via the [Issues](../../issues) tab.

## License
Copyright (c) 2020 SAP SE or an SAP affiliate company. All rights reserved. This file is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSES/Apache-2.0.txt) file.
