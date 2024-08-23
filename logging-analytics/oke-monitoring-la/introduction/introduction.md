# Logging Analytics Overview
## Introduction

Kubernetes provides a highly robust and extremely customizable platform for managing, automatically deploying and scaling containerized workloads. Building a monitoring and troubleshooting system for this entire environment is a very challenging task. Oracle Cloud Infrastructure (OCI) Logging Analytics bridges this monitoring gap by providing a one-click end-to-end Kubernetes monitoring solution for the underlying infrastructure, Kubernetes platform and cloud-native applications.

This live lab will cover setting up end-to-end monitoring for a sample Kubernetes cluster (OKE) which has workloads simulating various production issues. It will also take you through the steps for troubleshooting the issues in the Kubernetes Cluster. Finally you will visualize the data collected from the OKE Cluster through Dashboards.

Estimated Workshop Time: 01 hours 30 minutes

Watch the video below for a quick walk-through of the lab.
[Exploring Oracle Cloud Infrastructure Logging Analytics](videohub:1_dt55vn2d) 

### Objectives

In this workshop, you will learn how to:

* Connect to the existing Kubernetes to collect logs such as Kubernetes & Linux System logs, application/container logs and Kubernetes Objects logs & monitoring data.
* Understand & visualize the Kubernetes Cluster topology.
   ![kubernetes-cluster-topology](images/kubernetes-cluster-topology.png)
* Understand the data model of telemetry collected by Kubernetes Monitoring Solution.
* Visualize the data collected from the OKE Cluster through Dashboards like below.
     - ### Kubernetes Cluster Summary

        ![kubernetes-cluster-summary](images/kubernetes-cluster-summary.png)
     - ### Kubernetes Nodes

        ![kubernetes-nodes](images/kubernetes-nodes.png)
     - ### Kubernetes Pods

        ![kubernetes-pods](images/kubernetes-pods.png)
     - ### Kubernetes Workloads

        ![kubernetes-workloads](images/kubernetes-workloads.png)            


### Prerequisites

This lab assumes you have:

* Oracle.com SSO account.
* Understanding of Logging Analytics concepts.
* Understanding of Kubernetes/OKE concepts.
* Familiarity with OCI Console.


## Learn More

* [Monitor Kubernetes and OKE clusters with OCI Logging Analytics](https://docs.oracle.com/en/solutions/kubernetes-oke-logging-analytics/index.html)

* [Kubernetes Solution] (https://docs.oracle.com/en-us/iaas/logging-analytics/doc/kubernetes-solution.html)

* [Kubernetes Workloads] (https://kubernetes.io/docs/concepts/workloads/)


## Acknowledgements
* **Author** - Vikram Reddy , OCI Logging Analytics
* **Contributors** -  Vikram Reddy, Heena Rahangdale , OCI Logging Analytics
* **Last Updated By/Date** - Vikram Reddy, Aug, 2024
