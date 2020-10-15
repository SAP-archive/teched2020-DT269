# Exercise 1 - Setup connection between ITCM and Kyma runtime

In this exercise, you will setup a connection between ITCM and Kyma runtime, register ITCM domain events on Kyma runtime.

## Step 1.1 - Create a ITCM application in Kyma runtime

Create an ITCM application in Kyma cockpit.

![](/exercises/ex1/images/e1-create-app.png)

Binding ITCM application to a namespace.

![](/exercises/ex1/images/e1-create-app-binding.png)

## Step 1.2 - Register Kyma runtime in ITCM Extension Center

Register Kyma runtime in ITCM Extension Center system tab.

![](/exercises/ex1/images/e1-register-kyma.png)

## Step 1.3 - Register ITCM exposed domain event APIs on Kyma runtime

Expose domain event to Kyma runtime by a secure connection.

**To secure the connection, you need to generate a private key by OpenSSL tool and request a certificate signed by Kyma runtime.**
**The credential is mandatory for the communication with Kyma runtime.**
</br>Detail steps:
</br>![here](https://kyma-project.io/docs/components/application-connector/#tutorials-get-the-client-certificate)

Choose claims from categorized event on Event Mesh.
<br>![](/exercises/ex1/images/e1-events-list.png)

Event reference.
<br>![](/exercises/ex1/images/e1-events-detail.png)

Define a channel for event publishing.
<br>![](/exercises/ex1/images/e1-events-channel.png)

## Summary

Continue to - [Exercise 2 - Implement extensional functions in Kyma runtime](../ex2/README.md)

