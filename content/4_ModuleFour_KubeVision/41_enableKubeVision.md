---
title: "Enable KubeVision"
chapter: true
weight: 1
---

# 🔌 Activating KubeVision

KubeVision is Akuity's Kubernetes-native visibility tool that provides comprehensive insights across your clusters. Let's enable it for our workshop environment.

## Enable KubeVision for Your Cluster

::steps{name="enable-kubevision"}

1. Navigate to your Argo CD instance in the Akuity Platform

2. Click **Settings** in the top right corner

3. In the left sidebar, locate and click on **Features**

4. Find **KubeVision** in the features list

5. Toggle the switch to enable KubeVision for your Argo CD instance

6. Once enabled, you'll see a list of all clusters configured in your Argo CD instance

7. Enable KubeVision for your EKS cluster by toggling the switch next to it
   
   ![KubeVision Enabled](/images/KuebeVisionEnabled.png)

::

::alert[KubeVision collects data from your cluster to provide insights. This process may take a few minutes to fully populate all dashboards.]{header="Note"}

Once enabled, KubeVision will begin collecting data from your cluster. This information will be used to populate the various dashboards we'll explore in the next section.

::button[Continue to Dashboards Overview]{href="42_KubeVisionOverview.html" variant="primary"}
