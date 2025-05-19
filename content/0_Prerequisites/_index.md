---
title: Getting Started
weight: 1
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

::::tabs
:::tab{label="AWS Event"}
If you're attending an AWS hosted event (such as re\:Invent, an AWS Summit, or an AWS-organized online workshop), your environment will be provided for you [here](../0_Prerequisites/aws_event).

Your AWS instructor will provide you with:
- AWS account access
- Amazon EKS cluster details
- Additional workshop-specific instructions
:::

:::tab{label="Self-Paced"}
If you are running this workshop on your own, set up your environment [here](../0_Prerequisites/self_paced).

You'll need to:
- Create an AWS account if you don't have one
- Set up an Amazon EKS cluster
- Install required AWS CLI tools
- Configure AWS credentials
:::
::::

:::alert{header="Important" type="warning"}
If you are running this workshop on your own AWS account, remember to delete all AWS resources by following the [Clean Up Resources](../100_Conclusion/101_Clean_Up.md) section to avoid unnecessary charges.
:::

- Temporary AWS account credentials
- Pre-configured EKS cluster details
- Additional workshop-specific instructions

:::tab{label="Self-Paced"}
If you're running the workshop on your own, you'll need to set up the required AWS resources.

[Set up for self-paced workshop](./self_paced)

You'll need to:
- Use your own AWS account
- Create an EKS cluster
- Install and configure the necessary tools
- Follow additional setup instructions
::::

:::alert{header="Note"}
Choose the option that matches your situation. The workshop content is the same for both paths, but the initial setup differs.
:::
