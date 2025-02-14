---
title: "Set Up kubectl Access to EKS" # MODIFY THIS TITLE
chapter: true
weight: 1 # MODIFY THIS VALUE TO REFLECT THE ORDERING OF THE MODULES
---

<!-- MORE SUBMODULES CAN BE ADDED TO DIVIDE UP THE SETUP INTO SMALLER SECTIONS -->
<!-- COPY AND PASTE THIS SUBMODULE FILE, RENAME, AND CHANGE THE CONTENTS AS NECESSARY -->

# Set Up kubectl Access to EKS <!-- MODIFY THIS HEADING -->
<ol>
<li> Check to make sure your AWS CLI is authenticated by getting the name of your EKS cluster.

<pre><code> aws eks list-clusters
</code></pre>
The output should be similar to the following:
<pre><code> {
    "clusters": [
        "eksworkshop-eksctl"
    ]
}
</code></pre>

</li>
<li> Create a kubeconfig file for your cluster using the following command:

<pre><code> aws eks update-kubeconfig --name $(aws eks list-clusters | jq -r .clusters[0])
</code></pre>
The output should be similar to the following:
<pre><code> Added new context arn:aws:eks:us-east-1:338615488317:cluster/<cluster-name> to /home/vscode/.kube/config
</code></pre>

</li>
<li> Let's check to see if <code>kubectl</code> can access the cluster.

<pre><code> k get nodes
</code></pre>
The output should be similar to the following:
<pre><code> NAME                              STATUS   ROLES    AGE   VERSION
ip-192-168-108-33.ec2.internal    Ready    <none>   2d    v1.28.8-eks-ae9a62a
ip-192-168-158-117.ec2.internal   Ready    <none>   2d    v1.28.8-eks-ae9a62a
ip-192-168-182-251.ec2.internal   Ready    <none>   2d    v1.28.8-eks-ae9a62a
</code></pre>
</li>

</ol>