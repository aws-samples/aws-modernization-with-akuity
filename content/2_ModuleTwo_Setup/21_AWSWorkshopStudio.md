---
title: AWS + kubectl
weight: 1
---

## Authenticate AWS CLI
{{% notice warning %}}
You can skip this step if you're already authenticated.
{{% /notice %}}
1. In your terminal, enter this command: <code>aws configure </code>
2. You will be prompted to add your **AWS Access Key ID** and **AWS Secret Access Key**.
3. Set your default region.
4. You can verify if you're authenticated by using this command in the terminal:
<code>aws sts get-caller-identity</code>

## Set Up kubectl Access to EKS
Make sure you have <code>aws</code> and <code>kubectl</code> CLIs installed. If you're using a **Codespace** this should already be done for you. You'll need to configure the <code>kubectl</code> context to access your EKS cluster.
1. You can view your clusters in the terminal. <br>
Use the command: <pre><code>aws eks list-cluster</code></pre>
    The output should be similar to the following:
    <pre><code> {
    "clusters": [
        "eksworkshop-eksctl"
        ]
    }
    </code></pre>
2. Create a [kubeconfig file for your cluster](https://docs.aws.amazon.com/eks/latest/userguide/create-kubeconfig.html) using the following command:<br>
<pre><code>aws eks update-kubeconfig --name $(aws eks list-clusters | jq -r .clusters[0]) </code></pre>
    The output should be similar to the following:
    <pre><code>Added new context arn:aws:eks:us-east-1:338615488317:cluster/<cluster-name> to /home/vscode/.kube/config </code></pre>