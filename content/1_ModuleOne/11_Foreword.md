---
title: "Technical Issue: Why Use the Akuity Agent?" # MODIFY THIS TITLE
chapter: true
weight: 3 # MODIFY THIS VALUE TO REFLECT THE ORDERING OF THE MODULES IF APPLICABLE
---

#  Why Use the Akuity Agent Add-On?
Argo CD is typically used for managing both cluster add-ons and developer applications, but there's no surefire way to hook Argo CD up to everything. In a world without Akuity, this experience can be very custom and cumbersome. <br>
With the [Akuity Platform's unique agent architecture](https://akuity.io/blog/argo-cd-architectures-explained), we get to treat Argo CD as an add-on. Thus, other tooling like IaC or EKS add-on you can solve by bootstrapping ArgoCD into a cluster.<br>
 For those who have a strong preference for AWS, the Akuity AWS add-on decomplexifies the process with tighter integration and security, and also saves users the time of applying yaml, using API/CLI, or using IaC.