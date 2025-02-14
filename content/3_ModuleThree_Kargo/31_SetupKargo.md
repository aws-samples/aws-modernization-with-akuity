---
title: "Set Up Kargo Instance" # MODIFY THIS TITLE
chapter: true
weight: 1 # MODIFY THIS VALUE TO REFLECT THE ORDERING OF THE MODULES
---

## Set Up Your Kargo Instance
1. Let's head on over to the Akuity Platform and click the **Kargo** tab under the Argo CD tab.

2. On the top right, click **+ Create**

3. Go ahead and name your Kargo Instance, and add a description if you'd like. Once everything is fine and dandy, click **CREATE**.

4. You'll need to connect a Kargo Agent next. Go ahead and do so by clicking that **Register an Agent** button on the right.

5. Set the agent name, add a description, and then click the dropdown menu for **Akuity Managed Argo CD** and connect your Argo CD instance.

6. Click **Connect** once you're done.

7. Just like Argo CD, we'll need to set up an admin account. Click **Settings**, and go into **System Accounts**.

8. Enable admin accounts by hitting the switch, then set a password.

{{% notice info %}}
Put a pin in this!: keep your password handy, we'll need it to access the Kargo UI.
{{% /notice %}}

9. You can now access the Kargo UI via the instance URL displayed next to the Kargo Instance name.

