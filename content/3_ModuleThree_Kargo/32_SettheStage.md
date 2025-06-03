---
title: "Setting the Stage"
chapter: true
weight: 2
---

# 🎭 Setting Up Your Kargo Workflow

In this section, we'll configure the core components of Kargo: projects, warehouses, and stages.

## Understanding Kargo Concepts

Before we begin, let's understand the key concepts:

::::expand{header="Kargo Terminology"}
- **Project**: A collection of related Kargo resources that describes one or more delivery pipelines
- **Warehouse**: A source of Freight (versioned artifacts)
- **Freight**: A set of references to one or more versioned artifacts
- **Stage**: An environment in your application's lifecycle (e.g., dev, staging, production)
- **Promotion**: The process of moving Freight from one Stage to another
::::

## Creating a Kargo Project

1. Run the following command in your terminal:

   ```bash
   kargo create project kargo-guestbook
   ```

2. Check the Kargo UI - you should see a new project appear
   
   ![Created Project](/images/kargosavedproject.png)

## Setting Up GitHub Credentials

To allow Kargo to access your GitHub repository and make commits:

1. Run the following command in your terminal, replacing the placeholders with your information:

   ```bash
   kargo create credentials github-credentials \
   --project kargo-guestbook --git \
   --username $(gh api user | jq -r '.login')  --password ${KARGO_GH_TOKEN} \
   --repo-url $(gh repo view eks-workshop-template --json url  | jq -r .url)
   ```

2. Verify the credentials were created:

   ```
   secret/github-credentials created
   ```

   You can view your secrets in the top right corner of your Kargo Project's UI (marked with an asterisk *)
   
   ![Kargo secrets location](/images/KargoSecrets.png)

## Applying Your Project Configuration

1. Examine the `project.yaml` file in the `kargo` folder of your repository:

   ```yaml
   apiVersion: kargo.akuity.io/v1alpha1
   kind: Project
   metadata:
     name: kargo-guestbook
     annotations:
       # This annotation ensures Projects (Namespaces) are created first when deployed via Argo CD
       argocd.argoproj.io/sync-wave: "-1"
   ```

2. Apply this manifest to your Kargo project:

   ```bash
   cd /workshop/eks-workshop-template
   kargo apply -f ./kargo/project.yaml
   ```

## Creating a Warehouse

A Warehouse is a source of Freight (versioned artifacts) that Kargo will track and promote.

1. Examine the `warehouse.yaml` file in the `kargo` folder:

   ```yaml
   apiVersion: kargo.akuity.io/v1alpha1
   kind: Warehouse
   metadata:
     name: base
     namespace: kargo-guestbook
   spec:
     subscriptions:
     - git:
         branch: main
         commitSelectionStrategy: NewestFromBranch
         discoveryLimit: 20
         repoURL: https://github.com/<repo>
         includePaths:
         - base/values.yaml
   ```
   
   Update the `repoURL` with your repository name, replacing `<repo>` with your actual repository name (e.g., `your-username/eks-workshop-template`).
   
   ```bash
   sed -i "s?<repo>?${WORKSHOP_REPO}?g" /workshop/eks-workshop-template/kargo/warehouse.yaml
   ```

2. Apply this manifest to your Kargo project:

   ```bash
   kargo apply -f ./kargo/warehouse.yaml
   ```

3. Check the Kargo UI - you should now see a warehouse called "base"
   
   ![Finished Warehouse](/images/finishedwarehouse.png)

## Understanding Kargo Stages

::::expand{header="What are Stages?"}
Stages represent environments in your application's lifecycle, such as:
- Development ("dev")
- Staging ("stg")
- Production ("prd")

Each stage can have its own promotion steps, approval requirements, and validation processes.
::::

The `stages.yaml` file in your repository defines the promotion steps that Kargo will execute when promoting between stages:

1. **git-clone**: Clone the GitHub repository
2. **copy**: Copy values from `base/values.yaml` to `guestbook/values-dev.yaml`
3. **git-commit**: Commit the changes to the repository
4. **git-push**: Push the changes to GitHub
5. **argocd-update**: Update the changes in Argo CD

## Applying Your Stages

1. Update the `stages.yaml` file in the `kargo` folder with your repository name:

   ```bash
   sed -i "s?<repo>?${WORKSHOP_REPO}?g" /workshop/eks-workshop-template/kargo/stages.yaml
   ```

2. Apply the stages configuration:

   ```bash
   kargo apply -f ./kargo/stages.yaml
   ```

3. Check the Kargo UI - you should now see your stages configured
   
   ![Stages](/images/KargoIndex.png)

🎉 Congratulations! You now have a working Kargo pipeline with:
- A project to organize your resources
- A warehouse to track your artifacts
- Stages representing your environments
- Promotion steps to move changes between environments
