---
description: >-
  Deploying an Ampersand application in the cloud gives many benefits:
  continuous deployment, zero downtime, unlimited scalability. This is done on
  the Kubernetes platform.
---

# Deploying with Kubernetes

## Purpose

Deploying your Ampersand application to production can be done fast and frequent. For this purpose we are working on deployment on the Kubernetes platform. This allows you to deploy easily on your laptop \(for testing\), in your own data center \(The minimum you need is a virtual machiine that runs kubernetes\), or in the cloud \(to benefit from the reliability and security provided by hosting providers\). We use Kubernetes because it is open, free, well known, widely used, and is continuously being impoved by a large community. It lets you deploy fast and lets you upgrade the application without taking it offline.

## Way of working

1. You need a Kubernetes cluster, which you get from your provider, from your data center, or you create one yourself \(e.g. on your laptop\). A cluster is built on top of virtual or physical machines and hosts the services that expose \(i.e. to internet\).
2. 


## A use case

I tried it out for myself. First I got a cluster from Azure:



