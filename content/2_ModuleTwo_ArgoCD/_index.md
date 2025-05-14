---
title: "Deploy with Argo CD on EKS"
chapter: true
weight: 2
---

# 🚢 Deploy with Argo CD on Amazon EKS

![Argo CD](/images/ArgoCDLogoHorizontal.png)

## Continuous Delivery for Amazon EKS

In this module, we'll set up Argo CD on the Akuity platform to manage deployments to your Amazon EKS cluster. Argo CD implements GitOps principles, ensuring that your EKS cluster state matches the desired state defined in your Git repository.

### What You'll Learn

- How to configure kubectl to access your Amazon EKS cluster
- How to create and configure an Argo CD instance for EKS
- How to connect your EKS cluster to Argo CD using the AWS EKS add-on
- How to deploy applications to EKS using Helm charts
- How to implement auto-sync and self-healing capabilities for your EKS workloads

### Why This Matters for AWS Customers

Argo CD on Amazon EKS provides:

- **Declarative EKS deployments** - Define your desired state in Git
- **Automated synchronization** - Keep your EKS cluster in sync with your repository
- **Drift detection** - Identify and correct manual changes to EKS resources
- **Rollback capabilities** - Easily revert to previous states in your EKS cluster
- **Visualization** - See your application deployment status on EKS at a glance

Let's get started by setting up the Akuity Platform Agent AWS EKS Add-On to simplify the Argo CD instance creation process!
