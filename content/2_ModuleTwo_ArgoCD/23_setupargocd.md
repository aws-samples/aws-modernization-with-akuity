---
title: "Set Up Your Argo CD Instance" # MODIFY THIS TITLE
chapter: true
weight: 3 # MODIFY THIS VALUE TO REFLECT THE ORDERING OF THE MODULES
---

Let's move over to the Akuity Platform to set up your instance and connect our EKS add-on.

## Set Up an API Key for Your Instance
1. Select the Organization you want to create a key for, from the pull down menu.

2. Switch to the API Keys tab.

3. Click + New Key button on the lower right side of the page.

4. Set the Description for the key to workshop.

5. Assign the Owner Role to the key.

6. Click the Create button.

7. Click the Copy to Clipboard button, then paste and run the commands in the Codespace terminal.

## Create an Argo CD Instance
1. Navigate to Argo CD

2. Click + Create in the upper right hand corner of the dashboard.

3. Name your instance following the rules listed below the Instance Name field.

4. Click + Create.

Once you click create, your Argo CD instance will begin initializing. This takes about 2 minute. You'll know it's done when the cogwheel stops turning.

## Configure Your Instance
1. In the dashboard for the Argo CD Instance, click **Settings**.

2. On the sidebar on the right, under **Security & Access**, and then click **System Accounts**.

3. Enable **Admin Account** by clicking the toggle and clicking confirm when prompted.

4. Go ahead and set your admin password by clicking **Set Password**.

{{% notice info %}}
Put a pin in this!: keep your password handy, we'll need it to access the Argo UI.
{{% /notice %}}

5. To access your Argo CD Instance, click the instance URL, which may look like this:
```1241afhuahr2f.cd.akuity.cloud```

6. You'll be brought to the Argo CD login. **admin** is your user, and use the password you set in step 4.

## Configure Your Cluster
1. On your Argo CD Instance, click **Clusters**.

2. Click **Connect a Cluster**.

3. Set your cluster's name to your eks cluster.

4. Add a description (optional)

5. Click **Advanced Settings**

6. On the Add-Ons tab, you'll see two options: **Datadog**, and **AWS EKS**.

7. Make sure you click **+Add** on AWS EKS.

8. Go ahead and click **Connect Cluster** once you're done.

9. You'll be prompted to either use the AWS Console or AWS CLI to install the agent to your cluster. Follow the directions on whichever one you prefer.

10. Check that your target is the correct cluster by running this command:
```kubectl config current-context ```
The output should look something like this:
```shell
arn:aws:eks:us-east-1:338615488317:cluster/cluster-name
```

11. You can check the pods in the <code>akuity</code> namespace by using the command: <code>kubectl get pods -n akuity</code>
<br>
The output should look something like this:
```shell
NAME                                                       
akuity-agent-<replicaset-id>-<pod-id>                       1/1     Running   0          65s
akuity-agent-<replicaset-id>-<pod-id>                       1/1     Running   0          65s
argocd-application-controller-<replicaset-id>-<pod-id>      2/2     Running   0          65s
argocd-notifications-controller-<replicaset-id>-<pod-id>    1/1     Running   0          65s
argocd-redis-<replicaset-id>-<pod-id>                       1/1     Running   0          65s
argocd-repo-server-<replicaset-id>-<pod-id>                 1/1     Running   0          64s
argocd-repo-server-<replicaset-id>-<pod-id>                 1/1     Running   0          64s

```

Once you see that green heart before the cluster name on your Argo CD instance, it signifies that your cluster health is **Healthy**.<br>Now, your cluster is set up with the Akuity Platform Agent! Let's explore what Argo CD can do.