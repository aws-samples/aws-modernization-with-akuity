---
title: "Deploy Helm Charts"
chapter: true
weight: 3
---

# 📦 Deploying Helm Charts with Argo CD

Now that we have our Argo CD instance set up, let's deploy a sample application using a Helm chart from our template repository.

## Create an Application in Argo CD

1. Navigate to the Argo CD UI using your instance URL

2. In the VS Code Explorer panel (left sidebar), navigate to `/workshop/eks-workshop-template/apps/` and click on `guestbook-dev.yaml` to open it

3. Review the file and notice the placeholders that need to be replaced:
   - `<github-username>` - Your GitHub username
   - `<repo-name>` - The repository name (eks-workshop-template)
   - `<cluster-name>` - The cluster name (eks-cluster)

4. Now, let's update the application YAML template with your specific values:

   ```bash
   # Replace placeholders with actual values using sed
   export WORKSHOP_REPO=$(gh repo view eks-workshop-template --json url | jq -r .url  | awk -F'/' '{print $4"/"$5}')
   sed -i "s?<repo>?${WORKSHOP_REPO}?g" /workshop/eks-workshop-template/apps/guestbook-dev.yaml
   sed -i "s/demo/default/g" /workshop/eks-workshop-template/apps/guestbook-dev.yaml
   
   # Display the updated YAML file
   cat /workshop/eks-workshop-template/apps/guestbook-dev.yaml
   ```

5. Notice how the file in VS Code automatically updates with your actual values.

6. Click **+ NEW APP** in the top left corner of the Argo CD UI

7. Select **EDIT AS YAML** to use the YAML editor

8. Copy the contents of your updated YAML file and paste it into the editor

9. Click **SAVE** to convert the YAML into the form fields

10. Review the settings and click **CREATE** to create the application

    ![Complete App Card](/images/ArgoCDCompleteApplication.png)

:::alert{header="Note"}
The application status will initially show as **Missing** and **OutOfSync**. This is expected because we haven't synchronized it yet.
:::

## Synchronize Your Application

1. Click on your application card titled `argocd/guestbook-dev`

2. Click the **SYNC** button and then **SYNCHRONIZE** to deploy the resources defined in your application
   
   ![Sync](/images/ArgoCDSync.png)

The resource tree will expand as Argo CD creates the resources:
- The Deployment creates a ReplicaSet that creates a Pod
- The Service creates an Endpoint and EndpointSlice

The application will remain in "Progressing" state until the pod is running. Once complete, all top-level resources in the tree will show a green checkmark, indicating they are successfully synchronized.

## Update and Sync Changes Manually

Let's see how to deploy a new version of our application:

1. In the VS Code Explorer panel (left sidebar), navigate to your repository files

2. Open the file `eks-workshop-template/guestbook/values-dev.yaml` by clicking on it

3. In the editor, update the image tag from `0.1.0` to `0.2.0`:

   ```yaml
   # Before:
   image:
     tag: 0.1.0
   
   # After:
   image:
     tag: 0.2.0
   ```

4. Save the file (Ctrl+S or Cmd+S)

5. Commit and push these changes:

   ```bash
   cd /workshop/eks-workshop-template
   git add guestbook/values-dev.yaml
   git commit -m "Update guestbook image tag to 0.2.0"
   git push origin main
   ```

6. Return to the Argo CD UI and open your `argocd/guestbook-dev` application

7. Click **REFRESH** to trigger Argo CD to check for changes in your repository

8. Click **SYNC** then **SYNCHRONIZE** to deploy the changes

Argo CD will detect that the application is out-of-sync due to the change in the repository. It will template the Helm chart and patch the `guestbook-dev` deployment with the new image tag, triggering a rolling update.

![Updated Helm Chart](/images/ImageTagUpdated.png)

## Enable Auto-Sync and Self-Healing

Let's configure the application to automatically apply changes without manual intervention:

1. Click **APP DETAILS** in the top menu

2. Under the **SYNC POLICY** section, click **ENABLE AUTO-SYNC** and confirm by clicking **OK**

3. Below that, next to **SELF HEAL**, click **ENABLE**

With auto-sync enabled, any changes to the `main` branch in your repository will be automatically applied to the cluster. Self-healing ensures that any manual changes to the cluster resources will be reverted to match the desired state in Git.

## Demonstrate Auto-Sync via Git

Let's test the auto-sync feature by updating the number of replicas:

1. In the VS Code Explorer panel (left sidebar), navigate to your repository files

2. Open the file `eks-workshop-template/guestbook/values-dev.yaml` by clicking on it

3. In the editor, locate the `replicaCount` parameter at the top of the file and change its value from `1` to `2`:

   ```yaml
   # Before:
   replicaCount: 1
   
   # After:
   replicaCount: 2
   ```

4. Save the file (Ctrl+S or Cmd+S)

5. Commit and push your changes:

   ```bash
   cd /workshop/eks-workshop-template
   git add guestbook/values-dev.yaml
   git commit -m "Increase guestbook replicas to 2"
   git push origin main
   ```

6. Return to the Argo CD UI and open your `argocd/guestbook-dev` application

7. Click **REFRESH** to trigger Argo CD to check for changes

You can view the details of the sync operation by clicking **SYNC STATUS** in the top menu. This will show:
- Which revision was synchronized
- What triggered the sync (e.g., "INITIATED BY: automated sync policy")
- What resources were changed

## Deploy Staging And Production

Before we proceed, let's ensure that the `guestbook-stg` and `guestbook-prd` applications are deployed in Argo CD for the next module.
   
1. Replace the placeholders in the `guestbook-stg.yaml` and `guestbook-prd.yaml` files with your actual values:

   ```bash
   # Replace placeholders with actual values using sed
   sed -i "s?<repo>?${WORKSHOP_REPO}?g" /workshop/eks-workshop-template/apps/guestbook-stg.yaml
   sed -i "s/demo/default/g" /workshop/eks-workshop-template/apps/guestbook-stg.yaml
   sed -i "s?<repo>?${WORKSHOP_REPO}?g" /workshop/eks-workshop-template/apps/guestbook-prd.yaml
   sed -i "s/demo/default/g" /workshop/eks-workshop-template/apps/guestbook-prd.yaml
   ```

2. Apply the Argo CD Application YAMLs for staging and production:

   ```bash
   argocd app create -f /workshop/eks-workshop-template/apps/guestbook-stg.yaml
   argocd app create -f /workshop/eks-workshop-template/apps/guestbook-prd.yaml
   ```
   
   Feel free to check the Argo CD UI to confirm that the applications are created successfully. You can also synchronize them manually if you wish.

🎉 Congratulations! You've successfully:
- Created an Argo CD application
- Deployed a Helm chart
- Updated the application manually
- Configured auto-sync and self-healing
- Verified automatic synchronization
