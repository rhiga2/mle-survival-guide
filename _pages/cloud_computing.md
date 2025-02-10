---
title: Cloud Computing
author: Ryley Higa
date: 2025-02-03
category: cloud-computing
ordering: 010
layout: post
publish: false
---

# Introduction
## Why Cloud?
## Different Levels of Cloud Offerings
### Infrastructure as a Service
### Platform as a Service
### Serverless


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

# IAM

# Compute

# Virtual Private Cloud 
## IP Addresses and CIDR Notation

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
