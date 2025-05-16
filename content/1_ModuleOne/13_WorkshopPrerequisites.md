---
title: "Workshop Prerequisites"
chapter: true
weight: 4
---

# 📋 Workshop Prerequisites

## Background Knowledge

To get the most from this AWS workshop, it helps to have basic familiarity with:

::::tabs
:::tab{label="GitOps"}
GitOps is a set of practices that uses Git as the single source of truth for declarative infrastructure and applications.

[Learn more about GitOps](https://akuity.io/gitops)

![GitOps](/images/GitOps.png)
:::

:::tab{label="Amazon EKS"}
Amazon Elastic Kubernetes Service (EKS) is a managed Kubernetes service that makes it easy to run Kubernetes on AWS without needing to install, operate, and maintain your own Kubernetes control plane.

[Learn more about Amazon EKS](https://aws.amazon.com/eks/)
:::

:::tab{label="Argo CD"}
Argo CD is a declarative, GitOps continuous delivery tool for Kubernetes that follows the GitOps pattern of using Git repositories as the source of truth for defining the desired application state.

[Deployment made easy with Argo CD](https://akuity.io/blog/deployment-made-easy-with-argo-cd)
:::

:::tab{label="Kargo"}
Kargo is a promotion engine that helps you move code through different environments in a controlled, automated way.

[Promotion made easy with Kargo](https://akuity.io/blog/promotion-made-easy-with-kargo)
:::

:::tab{label="KubeVision"}
KubeVision provides enhanced visibility into your Kubernetes clusters, making monitoring and troubleshooting easier.

[Cluster monitoring with KubeVision](https://akuity.io/blog/cluster-monitoring-made-easy-with-kubevision-kubevision-for-beginners)
:::
::::

## Required Accounts and Resources

To complete this workshop, you'll need:

1. **GitHub Account** - [Create one here](https://github.com)
2. **GitHub CLI** - For repository operations (pre-installed in AWS Workshop Studio environments)
3. **Akuity Account** - [Sign up for a 30-day free trial](https://akuity.cloud)
4. **AWS Account** - Will be provided if this is an AWS co-hosted event
5. **Amazon EKS Cluster** - Will be provided if this is an AWS co-hosted event

![Akuity Login](/images/AkuityLogIn.png)

## Required CLI Tools

The following command-line tools should be installed:

1. **AWS CLI** - For interacting with AWS services
2. **kubectl** - For interacting with Kubernetes clusters
3. **git** - For source code management
4. **gh** - GitHub CLI for repository operations
5. **helm** - For managing Kubernetes applications

:::alert{header="Note"}
If you're using an AWS-provided environment for this workshop, these tools will already be installed.
:::
