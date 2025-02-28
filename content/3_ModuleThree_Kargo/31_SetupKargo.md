---
title: "Set Up Kargo Instance" # MODIFY THIS TITLE
chapter: true
weight: 1 # MODIFY THIS VALUE TO REFLECT THE ORDERING OF THE MODULES
---

## Set Up Your Kargo Instance
1. Let's head on over to the Akuity Platform and click the **Kargo** tab under the Argo CD tab.
<br>

2. On the top right, click **+ Create**
<br>

3. Go ahead and name your Kargo Instance ```kargo-demo``` and add a description if you'd like. Click **CREATE** when you're satisfied.
<br>

![Createinstance](../../static/images/KargoCreateInstance.png)

<br>


4. You'll need to connect a Kargo Agent next. Go ahead and do so by clicking that **Register an Agent** button on the right.
<br>


5. Set the agent name, add a description, and then click the dropdown menu for **Akuity Managed Argo CD** and connect your Argo CD instance you created earlier.
<br>

![ConnectKargoAgent](../../static/images/KargoRegisteranAgent.png)

<br>

6. Click **Connect** once you're done.
<br>

7. Just like Argo CD, we'll need to set up an admin account. Click **Settings**, and go into **System Accounts**.
<br>

8. Enable admin accounts by hitting the switch, then set a password. Hit **Save** on the top right. The cogwheel next to your Kargo Instance's name will start spinning.
<br>

![AdminAcc](../../static/images/KargoCreateAdminAcc.png)


<br>

{{% notice info %}}
Put a pin in this!: keep your password handy, we'll need it to access the Kargo UI.
{{% /notice %}}

1. Log in to Kargo CLI in your terminal with this command. Use the instance URL next to your Kargo instance's name (with https:// in front), and add your password you set in the last step: <br>
   
   
   ```shell

   kargo login https://<your instance URL> \
   --admin \
   --password <password> \
   --insecure-skip-tls-verify


:tada: You are now logged in to Kargo. Now let's set the stage...literally. :arrow_right:

