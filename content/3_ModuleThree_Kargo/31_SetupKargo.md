---
title: "Set Up Kargo Instance"
chapter: true
weight: 1
---

# 🚀 Creating Your Kargo Instance

Let's set up a Kargo instance to manage promotions between environments.

## Create a Kargo Instance



1. In the Akuity Platform, click the **Kargo** tab (located next to the Argo CD tab)

2. Click **+ Create** in the top right corner

3. Name your Kargo instance `kargo-demo` and optionally add a description

4. Click **CREATE** to initialize your instance
   
   ![Create instance](/images/KargoCreateInstance.png)


## Register a Kargo Agent



1. Click the **Register an Agent** button on the right side of the screen

2. Set a name for your agent (e.g., `workshop-agent`)

3. Optionally add a description

4. Click the dropdown menu for **Akuity Managed Argo CD** and select your Argo CD instance from the previous module
   
   ![Connect Kargo Agent](/images/KargoRegisteranAgent.png)

5. Click **Connect** to register the agent


## Configure Admin Access



1. Click **Settings** in the top navigation bar

2. Navigate to **System Accounts** in the left sidebar

3. Enable admin accounts by toggling the switch

4. Set a password for the admin account

5. Click **Save** in the top right corner
   
   ![Admin Account](/images/KargoCreateAdminAcc.png)

   ::alert[Keep this password handy! You'll need it to access the Kargo UI and CLI.]{header="Important"}


## Log in to Kargo CLI



1. In your terminal, run the following command:

   ```bash
   kargo login https://<your-instance-URL> \
   --admin \
   --password <password> \
   --insecure-skip-tls-verify
   ```

   Replace:
   - `<your-instance-URL>` with your Kargo instance URL (without the `https://` prefix)
   - `<password>` with the admin password you set earlier

2. Verify successful login (you should see a confirmation message)


🎉 Congratulations! You're now logged in to Kargo and ready to set up your promotion workflow.
