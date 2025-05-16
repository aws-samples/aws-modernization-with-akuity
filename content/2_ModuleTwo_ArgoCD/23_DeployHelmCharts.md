---
title: "Deploy Helm Charts"
chapter: true
weight: 3
---

# 📦 Deploying Helm Charts with Argo CD

Now that we have our Argo CD instance set up, let's deploy a sample application using a Helm chart from our template repository.

## Create an Application in Argo CD

:::steps
1. Navigate to the Argo CD UI using your instance URL

2. Click **+ NEW APP** in the top left corner

3. Select **EDIT AS YAML** to use the YAML editor

4. Paste the following YAML from the template in `apps/guestbook-dev.yaml`:

   ```yaml
   apiVersion: argoproj.io/v1alpha1
   kind: Application
   metadata:
     name: guestbook-dev
     namespace: argocd
   spec:
     project: default
     source:
       repoURL: 'https://github.com/<github-username>/<repo-name>'
       path: guestbook
       targetRevision: HEAD
       helm:
         valueFiles:
           - values-dev.yaml
     destination:
       namespace: guestbook-dev
       name: <cluster-name>
     syncPolicy:
       syncOptions:
         - CreateNamespace=true
   ```

5. Replace the placeholders:
   - `<github-username>` with your GitHub username
   - `<repo-name>` with your repository name (should be `akuity-eks-workshop`)
   - `<cluster-name>` with your cluster name (should be `eks-cluster`)

6. Click **SAVE** to convert the YAML into the form fields

7. Review the settings and click **CREATE** to create the application

   ![Complete App Card](/images/ArgoCDCompleteApplication.png)
:::

:::alert{header="Note"}
The application status will initially show as **Missing** and **OutOfSync**. This is expected because we haven't synchronized it yet.
:::

## Synchronize Your Application

:::steps
1. Click on your application card titled `argocd/guestbook-dev`

2. Click the **SYNC** button and then **SYNCHRONIZE** to deploy the resources defined in your application
   
   ![Sync](/images/ArgoCDSync.png)
:::

The resource tree will expand as Argo CD creates the resources:
- The Deployment creates a ReplicaSet that creates a Pod
- The Service creates an Endpoint and EndpointSlice

The application will remain in "Progressing" state until the pod is running. Once complete, all top-level resources in the tree will show a green checkmark, indicating they are successfully synchronized.

## Update and Sync Changes Manually

Let's see how to deploy a new version of our application:

:::steps
1. Navigate to `guestbook/values-dev.yaml` in your GitHub repository

2. Edit the `image.tag` value to update the version:

   ```yaml
   image:
     tag: 0.2.0
   ```

3. Commit these changes with a descriptive message

4. Return to the Argo CD UI and open your `argocd/guestbook-dev` application

5. Click **REFRESH** to trigger Argo CD to check for changes in your repository

6. Click **SYNC** then **SYNCHRONIZE** to deploy the changes
:::

Argo CD will detect that the application is out-of-sync due to the change in the repository. It will template the Helm chart and patch the `guestbook-dev` deployment with the new image tag, triggering a rolling update.

![Updated Helm Chart](/images/ImageTagUpdated.png)

## Enable Auto-Sync and Self-Healing

Let's configure the application to automatically apply changes without manual intervention:

:::steps
1. Click **APP DETAILS** in the top menu

2. Under the **SYNC POLICY** section, click **ENABLE AUTO-SYNC** and confirm by clicking **OK**

3. Below that, next to **SELF HEAL**, click **ENABLE**
:::

With auto-sync enabled, any changes to the `main` branch in your repository will be automatically applied to the cluster. Self-healing ensures that any manual changes to the cluster resources will be reverted to match the desired state in Git.

## Demonstrate Auto-Sync via Git

Let's test the auto-sync feature by updating the number of replicas:

:::steps
1. Navigate to your repository and open `guestbook/values.yaml`

2. Update the `replicaCount` value from `1` to `2`

3. Commit your changes

4. Return to the Argo CD UI and open your `argocd/guestbook-dev` application

5. Click **REFRESH** to trigger Argo CD to check for changes
   
   ![ReplicaSet Created](/images/ArgoCDReplicaSet.png)
:::

You can view the details of the sync operation by clicking **SYNC STATUS** in the top menu. This will show:
- Which revision was synchronized
- What triggered the sync (e.g., "INITIATED BY: automated sync policy")
- What resources were changed

🎉 Congratulations! You've successfully:
- Created an Argo CD application
- Deployed a Helm chart
- Updated the application manually
- Configured auto-sync and self-healing
- Verified automatic synchronization
