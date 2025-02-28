---
title: "Making Promotions"
chapter: true
weight: 3 # MODIFY THIS VALUE TO REFLECT THE ORDERING OF THE MODULES
---

## Time to Make Your First Promotion
Now that the stages are set, we can now make our first promotion. When we promote, we are moving the **freight** to the next stage, or environment. We can visualize where our code is moving through an application's lifecycle.

1. To make a promotion, click the blue **bullseye** icon on the left of the first stage, **dev**.

2. Select your **freight** on the top in the freight line. When prompted, select **yes**.
3. Watch the status next to **dev**. If it a full heart, your promotion was successful. If you receive a broken heart, it means there was an issue. You can click the stage and select the name of the promotion for more information on the error.

:tada: It's that easy to make a promotion in Kargo! 

## Making a replicaSet with Kargo
Like we did in Argo, we can create a replicaSet in Kargo. Navigate to the ```base/values.yaml``` in your repository. It should look something like this:
```yaml
replicaCount: 1
```
1. Change the value from 1 to 2.
<br>

2. Commit your changes.
<br>

3. Push your changes back to the repo, and refresh the Kargo UI.

You should see a replica sitting in the **Freight line** at the top. 
<br>
:thinking: We have some replicaSets, we have a cluster full of resources and namespaces we'll need to track. Select the next module to see how we can easily manage and monitor our cluster. :arrow_right: