---
title: "AWS EKS Challenges"
chapter: true
weight: 3
---

# 🔧 Solving Common EKS Challenges

## The Amazon EKS Complexity Challenge

While Amazon EKS provides a managed Kubernetes service that simplifies cluster operations, AWS customers still face challenges in:

- **Deployment management** - Maintaining consistency across AWS environments
- **Application promotion** - Moving code through development, staging, and production on AWS
- **Troubleshooting** - Identifying and resolving issues in EKS clusters quickly
- **Resource visibility** - Understanding EKS cluster state and resource utilization

## The AWS Marketplace Solution

AWS and Akuity have partnered to provide an all-in-one solution with the **Akuity Platform Agent** available as an EKS add-on through AWS Marketplace:

![AWS Marketplace Add-On](/images/AWSMarketplaceAkuity.png)

The **Akuity Platform Agent** installs directly into your Amazon EKS cluster and provides comprehensive solutions:

### 👁️ Enhanced EKS Visibility

Gain deeper insights into EKS cluster status, resources, and visualize deployments and code promotion workflows.

### 📏 Improved AWS Scalability

Akuity's unique [agent-based architecture](https://akuity.io/blog/argo-cd-architectures-explained) simplifies scaling across multiple AWS regions and accounts by running dedicated application controllers and repo servers in each manager cluster.

### 🔐 Better AWS Security

The agent-based architecture enables EKS clusters to access the Argo Control plane while keeping sensitive information safely inside the cluster, aligning with AWS security best practices.

### 🗂️ Streamlined EKS Resource Organization

Manage EKS cluster resources effortlessly with KubeVision, which exposes data already collected from your deployments for immediate access.

### 🔔 Proactive EKS Monitoring

When errors occur in your EKS clusters, they're logged in KubeVision with troubleshooting suggestions. Use the Timeline view to track cluster status and identify issues within specific timeframes.

::alert[AWS and Akuity have worked together to ensure the Akuity Platform integrates seamlessly with Amazon EKS through the AWS Marketplace, making it easy to add to your existing EKS clusters.]{header="AWS Integration"}
