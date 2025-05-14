---
title: Getting Started
weight: 20
---

# 🚀 Getting Started with the AWS Workshop

## Workshop Architecture

The following architecture diagram illustrates the AWS and Akuity components we'll be working with in this workshop:

![Architecture Diagram](/static/images/introduction/architecture.png)

## What You'll Build on AWS

In this workshop, you'll create a complete GitOps workflow on AWS using:

1. **Amazon EKS** - AWS's managed Kubernetes service
2. **Argo CD** - Declarative, GitOps continuous delivery for Kubernetes
3. **Kargo** - Streamlined promotion workflows across AWS environments
4. **KubeVision** - Advanced monitoring and troubleshooting capabilities for EKS

All of these components work together on AWS, with the Akuity Platform integrating seamlessly with Amazon EKS through the AWS Marketplace.

## Preparing for the Workshop

Follow the installation instructions in this section to prepare your AWS environment:

::tabs{name="setup-options"}

::tab{name="AWS Event" active=true}
If you are attending an AWS guided event, set up your environment [here](/02-getting-started/01-aws-event).

Your AWS instructor will provide you with:
- AWS account access
- Amazon EKS cluster details
- Additional workshop-specific instructions
::

::tab{name="Self-Paced"}
If you are running this workshop on your own, set up your environment [here](/02-getting-started/02-own-account).

You'll need to:
- Create an AWS account if you don't have one
- Set up an Amazon EKS cluster
- Install required AWS CLI tools
- Configure AWS credentials
::

::alert[If you are running this workshop on your own AWS account, remember to delete all AWS resources by following the [Clean Up Resources](/90-cleanup) section to avoid unnecessary charges.]{header="Important"}

::button[Start the Workshop]{href="/1_ModuleOne/_index.html" variant="primary"}
