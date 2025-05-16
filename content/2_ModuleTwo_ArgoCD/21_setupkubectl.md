---
title: "Setting up kubectl"
weight: 1
---

# 🔗 Connecting to Your EKS Cluster

Before we can deploy applications with Argo CD, we need to configure kubectl to communicate with your EKS cluster.

## AWS Authentication

:::alert{header="Note"}
Since you're using the VS Code server environment, AWS authentication is already configured with a role attached. You can skip the manual authentication steps.
:::

You can verify your AWS authentication by running:

```bash
aws sts get-caller-identity
```

You should see your AWS account information displayed, confirming that your environment is properly authenticated.

## Configure kubectl for EKS

Make sure you have the `aws` and `kubectl` CLIs installed. If you're using the Workshop Studio environment, these should already be available.

:::steps
1. List your available EKS clusters:

   ```bash
   aws eks list-clusters
   ```

   You should see output similar to:

   ```json
   {
     "clusters": [
       "akuity-aws-cluster"
     ]
   }
   ```

2. Create a kubeconfig file for your cluster:

   ```bash
   aws eks update-kubeconfig --name akuity-aws-cluster
   ```

   Alternatively, you can use this command to automatically use the first cluster in your account:
   
   ```bash
   aws eks update-kubeconfig --name $(aws eks list-clusters | jq -r .clusters[0])
   ```

   This should output:

   ```
   Added new context arn:aws:eks:us-east-1:123456789012:cluster/akuity-aws-cluster to /home/vscode/.kube/config
   ```

   ![Check Clusters](/images/ArgoCDCheckingClusters.png)

3. Test your kubectl access:

   ```bash
   kubectl get nodes
   ```

   You should see output similar to:

   ```
   NAME                              STATUS   ROLES    AGE   VERSION
   ip-192-168-108-33.ec2.internal    Ready    <none>   2d    v1.31.1-eks-ae9a62a
   ```
:::

::expand[
Let's break down the commands we used:

- `aws eks list-clusters` lists all EKS clusters in your current AWS account and region
- `$(aws eks list-clusters | jq -r .clusters[0])` is a sub-command that:
  - Executes first and provides the output as the value for the `--name` parameter
  - Uses the pipe symbol `|` to pass the output to the next command
  - Uses `jq -r .clusters[0]` to extract the first cluster name from the JSON output
- `aws eks update-kubeconfig` updates your kubeconfig file with the credentials needed to access the specified cluster
]{header="Understanding the kubectl Configuration Command"}

Now that kubectl is configured to access your EKS cluster, you're ready to set up your Argo CD instance!
