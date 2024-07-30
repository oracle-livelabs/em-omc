# Logging Analytics Overview
## Introduction

> Note : To be updated with ocw-24 introduction.

Kubernetes provides a highly robust and extremely customizable platform for managing, automatically deploying and scaling containerized workloads. Building a monitoring and troubleshooting system for this entire environment is a very challenging task. Oracle Cloud Infrastructure (OCI) Logging Analytics bridges this monitoring gap by providing a one-click end-to-end Kubernetes monitoring solution for the underlying infrastructure, Kubernetes platform and cloud-native applications.

This live lab will cover setting up end-to-end monitoring solution for a sample Kubernetes cluster (OKE cluster) which has [MuShop] (https://oracle-quickstart.github.io/oci-cloudnative/) (a cloud-native reference application of several Oracle Cloud services) deployed. It also takes you through various visualizations and perform analytics over the collected data from different perspectives.

Estimated Workshop Time: 01 hours 30 minutes

Watch the video below for a quick walk-through of the lab.
[Exploring Oracle Cloud Infrastructure Logging Analytics](videohub:1_dt55vn2d) 

### Objectives

In this workshop, you will learn how to:

* Install OCI Kubernetes Monitoring Solution to collect Kubernetes & Linux System logs, application/container logs and Kubernetes Objects logs.
* Set up Management Agent to collect Kubernetes metrics and reporting them to OCI Monitoring.
* Understand the data model of telemetry collected by Kubernetes Monitoring Solution.
* Review the log data for specific MuShop logs in Log Explorer.
* Visualize the data collected from the OKE Cluster through Dashboards like below.
     - ### Kubernetes Cluster Summary

        ![kubernetes-cluster-summary](images/kubernetes-cluster-summary.png)
     - ### Kubernetes Nodes

        ![kubernetes-nodes](images/kubernetes-nodes.png)
     - ### Kubernetes Pods

        ![kubernetes-pods](images/kubernetes-pods.png)
     - ### Kubernetes Workloads
     
        ![kubernetes-workloads](images/kubernetes-workloads.png) 
* Perform advanced analytics to correlate Infrastructure (LBaaS) and K8S Platform telemetry.             


### Prerequisites

This lab assumes you have:

* Oracle.com SSO account
* Understanding of Logging Analytics concepts
* Understanding of Kubernetes/OKE concepts and helm
* Familiarity with OCI cloud shell and OCI Console


## Learn More

* [Monitor Kubernetes and OKE clusters with OCI Logging Analytics](https://docs.oracle.com/en/solutions/kubernetes-oke-logging-analytics/index.html)
* [MuShop] (https://oracle-quickstart.github.io/oci-cloudnative/)

## Acknowledgements
* **Author** - Vikram Reddy , OCI Logging Analytics
* **Contributors** -  Vikram Reddy, Santhosh Kumar Vuda , OCI Logging Analytics
* **Last Updated By/Date** - Vikram Reddy, Aug, 2023
