---
title: "Set Up Your Argo CD Instance"
chapter: true
weight: 2
---

# 🚀 Creating Your Argo CD Instance

Now that we have kubectl access to our EKS cluster, let's set up an Argo CD instance on the Akuity platform.

## Create an Argo CD Instance

1. Log in to the [Akuity Platform](https://akuity.cloud) and navigate to **Argo CD**

2. Click **+ Create** in the upper right corner of the dashboard

3. Enter a name for your instance (e.g., `workshop-argocd`)

4. Optionally add a description to help identify this instance

   ![Argo CD Create an Instance](/images/ArgoCDCreateanInstance2.png)

5. Click **+ Create** to initialize your instance

::alert[Your Argo CD instance will begin initializing. This process takes a few minutes. You'll know it's complete when the cogwheel next to your instance name stops turning and the status shows a 💚 healthy indicator.]{header="Note"}

## Configure Your Argo CD Admin Account

1. In the dashboard for your Argo CD instance, click **Settings**

2. On the sidebar, under **Security & Access**, click **System Accounts**

3. Enable the **Admin Account** by clicking the toggle and confirming when prompted

4. Set your admin password by clicking **Set Password**
   
   ![Set Password](/images/ArgoCDSetPassword.png)

   ::alert[Keep this password handy! You'll need it to access the Argo CD UI.]{header="Important"}

5. Wait for Argo CD to reinitialize (the cogwheel will spin and then stop)

6. Access your Argo CD instance by clicking the instance URL in the **Summary** tab
   
   Your URL will look similar to: `123456letters.cd.akuity.cloud`

7. At the Argo CD login screen, enter `admin` as the username and use the password you set in step 4

   ![Argo CD Login](/images/ArgoCDLogin.png)

8. On your terminal, login to your Argo CD instance using the CLI:

    ```bash
    argocd login --grpc-web --username admin <your-argocd-instance-url>
    ```

    Replace `<your-argocd-instance-url>` with your instance URL, which similar to: `123456letters.cd.akuity.cloud`.

## Connect Your EKS Cluster

1. Navigate back to your [Akuity Argo CD Instance](https://akuity.cloud) click **Clusters**

2. Click **Connect a Cluster**

3. Set your cluster name to `eks-cluster`

4. Optionally add a description with your EKS cluster's name

5. Click **Connect Cluster** to proceed

6. You'll be prompted to install the agent using either the AWS Console or AWS CLI
   
   ![Install Akuity Agent](/images/AkuityAgent.png)
   
   Follow the instructions for your preferred method

7. Verify you're targeting the correct cluster:

    ```bash
    kubectl config current-context
    ```

    The output should look similar to:
    ```
    arn:aws:eks:us-east-1:123456789:cluster/akuity-aws-cluster
    ```

8. Check that the Akuity agent pods are running:

    ```bash
    kubectl get pods -n akuity
    ```

    You should see output similar to:
    ```
    NAME                                                       READY   STATUS    RESTARTS   AGE
    akuity-agent-<replicaset-id>-<pod-id>                      1/1     Running   0          65s
    akuity-agent-<replicaset-id>-<pod-id>                      1/1     Running   0          65s
    argocd-application-controller-<replicaset-id>-<pod-id>     2/2     Running   0          65s
    argocd-notifications-controller-<replicaset-id>-<pod-id>   1/1     Running   0          65s
    argocd-redis-<replicaset-id>-<pod-id>                      1/1     Running   0          65s
    argocd-repo-server-<replicaset-id>-<pod-id>                1/1     Running   0          64s
    argocd-repo-server-<replicaset-id>-<pod-id>                1/1     Running   0          64s
    ```

::alert[When you see a 💚 green heart before the cluster name in your Argo CD instance, it indicates that your cluster is healthy and properly connected.]{header="Success"}

🎉 Congratulations! Your cluster is now set up on the Akuity Platform. The cluster data is uploaded to the platform, so we don't need to repeat this process for Kargo and KubeVision.
