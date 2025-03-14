---
title: Cloud Computing
author: Ryley Higa
date: 2025-02-03
category: cloud-computing
ordering: 010
layout: post
---

# Introduction
## What is Cloud Computing?
* Using remote servers to process, store, and manage data as opposed to local infrastructure.
* Cloud provider manage these remote servers and allow us to access these servers. 
* Examples of cloud providers include: Amazon Web Service (AWS), Google Cloud Provider (GCP), and Microsoft Azure.
* Virtualization
* Multi-tenancy: cloud users may share physical resources. 
## Why Cloud?
* Scalability (Elasticity): We can provision resources based on demand. 
* Availability: Cloud providers have data centers in many regions and availability zones. We can still be available when data centers go down. 
* Specialization: We don't need to worry about managing physical resources. Let the cloud provider handle it. 
## Different Levels
### Infrastructure as a Service
* Infrastructure is managed for you by a cloud provider, but you must manage the OS, libraries, and application.
### Platform as a Service and Serverless
* Infrastructure, OS, and many libraries are managed for you, but you must manage the application.
* Serverless compute is a type of PAAS that focuses on function execution. It's also known as function as a service. 
### Software as a Service
* Infrastructure, OS, application, etc... are managed for you.

# Identity and Access Management (IAM)
* Authentication: who are you? 
* Authorization: what can you do? 
* Shared Responsibility Model: cloud provider manages security of the cloud, but it's the users job to ensure security in the cloud.
* Principle of Least Privelege: only provide enough permissions to get the job done. 
## Policies, Users, Groups, and Roles
* Policies: Grant permissions to principals 
* Users: principals with long-term credentials
* Groups: Allow you to assign permissions to multiple users.
* Roles: principals can gain short-term credentials by assuming roles.

# Virtual Private Cloud 
## IP Addresses and CIDR
* IPv4
* IPv6
* CIDR specifies a range of ip addresses using the following notation
```
<ip_address>/<mask bits>
```
  * Mask bits refer to the number of bits left to right that are constant in the range. Higher mask bits means smaller range. 
## Public and Private Subnets
* Public subnets have a direct route to the internet gateway, whereas private subnets do not.
* Private subnets must use a NAT gateway to allow outbound connections to internet. Arbitrary inbound connections from the internet are not allowed.

# Cloudonomics
* More economical to use cloud if (average demand) * (cloud cost) < (peak demand) * (owning cost)
* Utility premium is cost ratio between renting versus buying (cloud cost / owning cost).
* Thus utility premium must be less than the ratio of peak demand over average demand.
* If demand varies and peak >> average, cloud computing is more cost efficient.
* Smoothness measure: coefficient of variation $C_V = \sigma / \mu$
* Aggregated CoV 
  * Increasing independent jobs decreases CoV by $1/\sqrt{n}$.
  * Jobs correlated negatively. CoV decreases
  * Jobs correlated positvely. CoV increases

# Compute

# Serverless Compute
* Build and launch applicaiton without managing the server yourself.
* Categories of Serverless Compute
  * PAAS (Apps) (i.e. Elastic Beanstalk, Google App Engine, IBM CloudFoundry)
  * Functions as a Service (Functions, what most people think of serverless) (AWS Lambda, Azure Functions, Google Cloud Functions)
    * Must be stateless 
  * Container as a Service (Containers): Funcs as a service on steroids. (EKS, ECS, Google Cloud Runs, Microsoft AKS) 
* Categories of Serverless Storage
  * Blob (binary large objects) (S3)
  * Key-Value Store (DynamoDB)
* Other Categories
  * AI and ML
  * Analytics
* What is serverless architecure?
  * Extension of PaaS   
  * Server-side logic is decomposed into components or containers that are triggered by events (event-driven), stateless, and ephemeral
  * States are retrieved at the beginning of computation and stored at the end computation. 
  * Pay per usage as opposed to PAAS

## AWS Step Functions (NEEDs more concreteness, section is too abstract at the moemnt!)
* Break workflow into smaller tasks. Can replay and rollback tasks
* Coordinate distributed apps
* Manage complex state transitions
* Visual workflows for easire debugging
### Terminology
* States define what happens next
* Tasks invoke work (i.e. lambda)
* Transitions manage workflow paths
* Can visualize as a DAG
* Standard: long running workflows
* Express: high volume

## API Gateway
* Frontdoor for serverless applications
* Handles multiple API types: REST, HTTP, WebSocket APIs
* Client makes call to API gateway, gateway invokes lambda function, S3, and EC2
* Methods, resources
* Stages and lifecyles of APIs (dev, test, prod)
* Auto-scaling
* Request/response mapping templates
* Security (IAM, cognito)
* Caching and throttling
* VPC link integration
* 
