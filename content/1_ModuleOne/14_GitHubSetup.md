---
title: "GitHub Repository Setup"
chapter: true
weight: 6
---

# 🔄 Setting Up Your GitHub Repository

## Why GitHub for GitOps?

GitOps uses Git repositories as the single source of truth for declarative infrastructure and applications. For this workshop, we'll use GitHub to:

1. Store our application manifests and Helm charts
2. Trigger deployments to our Amazon EKS cluster via Argo CD
3. Manage promotions between environments with Kargo

## GitHub Authentication

Let's start by authenticating with GitHub:

1. Check if you're already authenticated with GitHub:

   ```bash
   gh auth status || gh auth login
   ```

2. If you need to authenticate, follow these steps:
   - Select **GitHub.com**
   - Select **HTTPS** as your preferred protocol
   - When asked "Authenticate Git with your GitHub credentials?": Enter **Y**
   - Select **Login with a web browser**
   - Copy the one-time code shown in your terminal
   - Press Enter to open the browser
   - Paste the code in GitHub and authorize access
   - Return to your terminal and wait for authentication to complete (This can take up to 30 seconds or more)

![GitHub CLI Authentication](/images/gh-auth.png)

::alert[If you don't have the GitHub CLI installed, you can install it with the [installation instructions](https://github.com/cli/cli#installation) for your operating system.]{header="Note"}

## Fork the Workshop Repository

For this workshop, we'll fork the Akuity EKS workshop template repository. **Choose ONE of the following methods**:

### Option 1: Using GitHub CLI (Recommended)

Fork and clone the repository using the GitHub CLI:

```bash
# Fork the repository and clone it
gh repo fork akuity/eks-workshop-template --clone=true --remote=true
cd eks-workshop-template
```

### Option 2: Using GitHub Web Interface

If you prefer to use the GitHub web interface instead:

1. Visit [https://github.com/akuity/eks-workshop-template](https://github.com/akuity/eks-workshop-template)
2. Click the "Fork" button in the top-right corner
3. Ensure your personal account is selected as the owner
4. Keep the repository name as `eks-workshop-template`
5. Click "Create fork"
6. Clone the repository to your local machine:
   ```bash
   git clone https://github.com/YOUR-USERNAME/eks-workshop-template.git
   cd eks-workshop-template
   ```

## Create a GitHub Personal Access Token (PAT)

Kargo will need a GitHub Personal Access Token to make commits to your repository:

1. Go to [GitHub Settings > Developer settings > Personal access tokens > Fine-grained tokens](https://github.com/settings/tokens?type=beta)

2. Click "Generate new token"

3. Set the following:
   - Token name: `akuity-workshop`
   - Expiration: 7 days (or your preferred duration)
   - Repository access: Select "Only select repositories" and choose your forked repository
   - Permissions:
     - Repository permissions:
       - Contents: Read and write
       - Metadata: Read-only

4. Click "Generate token"

5. **Important**: Copy the generated token and store it securely. You'll need it when setting up Kargo.

::alert[Keep your Personal Access Token secure! It provides access to your GitHub account with the permissions you specified.]{header="Security Warning" type="warning"}

## Verify Repository Structure

Let's examine the repository structure to understand what we'll be working with:

1. Make sure you're in the repository directory:

   ```bash
   cd eks-workshop-template
   ```

2. List the key directories:

   ```bash
   ls -la
   ```

3. You should see directories including:
   - `guestbook/` - Contains the Helm chart for our sample application
   - `base/` - Contains base configuration values
   - `kargo/` - Contains Kargo configuration files
   - `apps/` - Contains application YAML files
   - `akuity-platform/` - Contains ArgoCD configuration files

## Repository Structure Explained

- **guestbook/** - The main application Helm chart
  - `Chart.yaml` - Helm chart metadata
  - `values.yaml` - Default values for the chart
  - `values-dev.yaml` - Development environment values
  - `values-staging.yaml` - Staging environment values
  - `values-prod.yaml` - Production environment values
  - `templates/` - Kubernetes manifest templates

- **base/** - Base configuration that will be promoted through environments
  - `values.yaml` - Base values that Kargo will copy to environment-specific files

- **kargo/** - Kargo configuration
  - `project.yaml` - Defines the Kargo project
  - `warehouse.yaml` - Configures the source of artifacts (your Git repo)
  - `stages.yaml` - Defines the promotion stages and steps

Now that your GitHub repository is set up, you're ready to create your Akuity account and connect it to your Amazon EKS cluster!
