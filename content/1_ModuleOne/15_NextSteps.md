---
title: "Akuity Account Setup"
chapter: true
weight: 7
---

# 🛠️ Setting Up Your Akuity Account

Now that you've set up your GitHub repository, let's create and configure your Akuity account to manage your Amazon EKS cluster.

## Creating Your Akuity Account

:::steps
1. Visit [akuity.cloud](https://akuity.cloud) to create an account
   ![Akuity Sign On](/images/AkuityCreateAccount.png)

2. Choose to sign in with your **email**, **GitHub**, or **Google Account**

3. After creating your account, you'll be prompted to create an [organization](https://akuity.io/blog/introducing-akuity-workspaces)
   ![Akuity First Sign Up](/images/AkuityFirstPage.png)

4. Click on the **Organization** tab to get started
   ![Organization Page](/images/AkuityOrganizationsPage.png)

5. Click **New Organization** in the top right corner
   ![Create an Organization](/images/AkuityCreateOrganization.png)

6. Enter a name for your organization (e.g., `aws-workshop`) and click **Create**
:::

## Understanding Akuity Organizations

::expand[
An Akuity Organization is a top-level container for your Akuity resources. It allows you to:

- Group related projects and clusters
- Manage user access and permissions
- Configure shared settings
- Track usage and billing

Organizations are particularly useful in enterprise environments where you might have multiple teams or projects using the Akuity Platform.
]{header="What is an Akuity Organization?"}

## What's Next?

Now that you have:
1. Set up your GitHub repository with the workshop template
2. Created a GitHub Personal Access Token for Kargo
3. Created your Akuity account and organization

You're ready to move on to the next module, where we'll:
1. Configure kubectl to access your Amazon EKS cluster
2. Create an Argo CD instance on the Akuity Platform
3. Connect your EKS cluster to Argo CD
4. Deploy your first application using GitOps principles

🎉 Congratulations! Your **Akuity Account** is now ready to deploy, promote, and monitor your Amazon EKS cluster.
