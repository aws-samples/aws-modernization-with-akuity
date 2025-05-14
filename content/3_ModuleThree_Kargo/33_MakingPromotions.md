---
title: "Making Promotions"
chapter: true
weight: 3
---

# 🚀 Promoting Changes with Kargo

Now that we have our Kargo pipeline set up, let's make our first promotion to move changes between environments.

## Your First Promotion

::steps{name="first-promotion"}

1. In the Kargo UI, locate the blue **bullseye** icon on the left side of the first stage (**dev**)
   
2. Click the bullseye to initiate a promotion

3. Select your **freight** from the freight line at the top of the screen

4. When prompted to confirm the promotion, select **yes**

5. Monitor the status next to the **dev** stage:
   - A full heart indicates a successful promotion
   - A broken heart indicates an issue (click on the stage and select the promotion name for error details)

::

::alert[Promotions in Kargo are tracked and auditable. You can see who promoted what and when, providing valuable traceability for your deployment process.]{header="Promotion Tracking"}

## Creating a ReplicaSet with Kargo

Just as we did with Argo CD, we can modify the number of replicas using Kargo's promotion workflow:

::steps{name="update-replicas"}

1. Navigate to `base/values.yaml` in your GitHub repository

2. Change the `replicaCount` value from `1` to `2`:

   ```yaml
   replicaCount: 2
   ```

3. Commit your changes

4. Push your changes back to the repository

5. Refresh the Kargo UI

::

You should now see a new freight item in the freight line at the top of the Kargo UI, representing your updated configuration.

## Understanding the Promotion Process

When you promote this change:

1. Kargo will detect the change in the `base/values.yaml` file
2. The promotion steps will:
   - Clone your repository
   - Copy the updated values to the target environment's values file
   - Commit and push the changes
   - Trigger Argo CD to update the deployment

This ensures a consistent, automated process for moving changes through your environments.

🎉 Congratulations! You've successfully:
- Set up a Kargo promotion workflow
- Made your first promotion
- Updated a configuration value that will be promoted through your environments

::button[Continue to Module 4: Monitor with KubeVision]{href="/4_ModuleFour_KubeVision/_index.html" variant="primary"}
