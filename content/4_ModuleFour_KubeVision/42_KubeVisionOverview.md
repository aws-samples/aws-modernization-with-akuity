---
title: "KubeVision Dashboards"
chapter: true
weight: 2
---

# 📊 Exploring KubeVision Dashboards

KubeVision provides several specialized dashboards to help you monitor and manage your Kubernetes clusters. Let's explore each one.

## Explorer Dashboard

![Explorer Dashboard](/images/KubeVisionExplorer.png)

The Explorer Dashboard is your central hub for browsing cluster resources. It provides a comprehensive view of all resources in your cluster, organized in a way that makes them easy to find and understand.

### Customizing Your View

You can tailor the Explorer Dashboard to your specific needs using the dropdown filters at the top:

![Explorer Dropdown](/images/KubeVisionExplorer2.png)

Filter by:
- Namespace
- Resource type
- Status
- Labels
- And more

:::alert{header="Tip"}
The Explorer Dashboard is a great starting point for investigating issues or getting a high-level overview of your cluster's resources.
:::

## Deprecated APIs Dashboard

![Deprecated APIs](/images/KubeVisionDeprecatedApis.png)

The Deprecated APIs Dashboard helps you identify and address obsolete Kubernetes APIs in your cluster. This is crucial for maintaining compatibility with future Kubernetes versions.

### Proactive API Management

For each deprecated API, KubeVision provides:
- The current API version being used
- The recommended replacement API version
- The number of resources affected
- When the API will be removed

![Deprecated APIs Details](/images/KubeVisionDeprecatedAPIs2.png)

## Stuck in Deletion Dashboard

This specialized dashboard identifies resources that have been stuck in the deletion state for more than 1 hour. These resources can cause issues with cluster management and should be addressed.

::::expand{header="Common Causes for Stuck Deletions"}
Resources can get stuck in deletion due to:
- Finalizers that haven't completed
- Dependencies that haven't been resolved
- Custom resource controllers that aren't functioning properly
- Networking issues preventing proper cleanup
::::

## Container Dashboard

![Container Dashboard](/images/KubeVisionContainers.png)

The Container Dashboard provides detailed information about all containers running in your cluster, with powerful filtering capabilities.

### Resource Utilization Insights

Filter containers by:
- Resource usage
- Resource limits
- Resource requests

![Containers Resources](/images/KubeVisionContainersResource.png)

You can sort by memory or CPU usage (click the arrows next to "Memory") to quickly identify the most resource-intensive containers. This is invaluable for optimizing resource allocation and identifying potential issues.

## Image Dashboard

![Images Dashboard](/images/KubeVisionImages.png)

The Image Dashboard provides comprehensive information about all container images used in your cluster.

### Image Details

For each image, you can see:
- Image name
- Number of containers using the image
- Image tags (to identify different versions)
- Digest (if applicable)
- CVEs (Common Vulnerabilities and Exposures)

![CVE Information](/images/KubeVisionCVEs.png)

:::alert{header="Security Note"}
CVE scanning is available for public images. Enable CVE scanning in KubeVision settings to identify potential security vulnerabilities.
:::

You can also find CVE information in the **Security** tab of your Argo CD instance.

## Infrastructure Dashboard

![Infrastructure Pods](/images/InfrastructurePods.png)

The Infrastructure dashboard offers two perspectives: **Pods** and **Nodes**.

### Pods View

In the Pods view, you can group by:
- Cluster
- Availability Zone
- Region
- Node

![Pods View](/images/InfrastructurePodsrunning.png)

### Nodes View

In the Nodes view, you can group by:
- CPU Utilization
- Memory Utilization
- Pod Count
- Pod Utilization

![Infrastructure Nodes](/images/InfrastructureNode.png)

This dashboard is particularly useful for understanding how your workloads are distributed across your infrastructure and identifying potential imbalances.

## Timeline View

![Timeline](/images/KubeVisionTimeline1.png)

The Timeline view captures events and errors in real-time, providing a chronological view of what's happening in your cluster.

### Event Tracking

You can:
- Set the time period for displayed events
- Filter by event type
- Search for specific events

The timeline shows critical workload events, which is invaluable for troubleshooting deployment failures, promotion issues, cluster health changes, and more.

![Timeline Details](/images/KubeVisionTimeline2.png)

Yellow circles with Kargo's logo indicate issues with Kargo. Clicking on these events provides detailed information about what went wrong and when.

## AI Assistant

![AI Assistant](/images/AkuityAssistant.png)

KubeVision includes an AI-powered assistant that can analyze your Kubernetes resources and provide insights and suggestions.

### Enabling the AI Assistant

1. Navigate to your Argo CD instance

2. Click the cogwheel in the top right for **Settings**

3. Under **General**, click **Extensions**
   
   ![Extensions](/images/AkuityExtensions.png)

4. Find **Akuity Assistant** and click **Install**

5. Once installed, go to the **Explorer** dashboard and click on any resource

6. A new **Assistant** tab will appear, allowing you to ask questions about the resource
   
   ![AI Assistant Details](/images/AkuityAIAssist2.png)

The AI Assistant can help you:
- Analyze deployment logs
- Review deployment issues
- Suggest optimizations
- Explain resource configurations
- Provide troubleshooting guidance