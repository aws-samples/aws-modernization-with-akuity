---
title: "Cleanup"
chapter: false
weight: 101
---

# 🧹 Comprehensive Cleanup

To avoid incurring unnecessary charges, follow these steps to clean up all resources created during the workshop.

::alert[**IMPORTANT**: You must run the cleanup commands in AWS CloudShell, NOT in the VS Code server environment. The VS Code server will be deleted as part of this cleanup process.]{header="Warning" color="warning"}

## 1. Clean Up Akuity Platform Resources

First, let's clean up the resources we created on the Akuity Platform:

### Disable KubeVision

1. Navigate to your Argo CD instance in the [Akuity Platform](https://akuity.cloud)
2. Click **Settings** in the top right corner
3. In the left sidebar, click on **Features**
4. Find **KubeVision** in the features list
5. Toggle the switch to disable KubeVision for your Argo CD instance

### Delete Kargo Instance

1. In the Akuity Platform, click the **Kargo** tab
2. Select your Kargo instance (`kargo-demo`)
3. Click **Settings** in the top navigation bar
4. Scroll to the bottom and click **Delete Instance**
5. Confirm deletion by typing the instance name

### Delete Argo CD Instance

1. In the Akuity Platform, click the **Argo CD** tab
2. Select your Argo CD instance (`workshop-argocd`)
3. Click **Settings** in the top navigation bar
4. Scroll to the bottom and click **Delete Instance**
5. Confirm deletion by typing the instance name

## 2. Launch AWS CloudShell

1. Open the [AWS Management Console](https://console.aws.amazon.com/)
2. Click the CloudShell icon in the top navigation bar or navigate directly to [CloudShell](https://console.aws.amazon.com/cloudshell/)
3. Wait for CloudShell to initialize

![AWS CloudShell](/images/aws-cloudshell.png)

## 3. Delete AWS CloudFormation Stacks

Delete the CloudFormation stacks that were created for this workshop:

### Using the AWS Management Console

1. Open the [AWS CloudFormation console](https://console.aws.amazon.com/cloudformation/)
2. Select the EKS cluster stack (typically named with `akuity-aws-cluster`)
3. Click **Delete** and confirm the deletion
4. Select the VS Code server stack
5. Click **Delete** and confirm the deletion

### Using the AWS CLI in CloudShell

```bash
# Delete the EKS cluster stack
aws cloudformation delete-stack --stack-name akuity-aws-cluster

# Delete the VS Code server stack
aws cloudformation delete-stack --stack-name vscode-server

# Wait for stack deletion to complete (optional)
aws cloudformation wait stack-delete-complete --stack-name akuity-aws-cluster
aws cloudformation wait stack-delete-complete --stack-name vscode-server
```

::alert[The stack deletion process may take 15-20 minutes to complete, especially for the EKS cluster stack.]{header="Note"}

## 4. Verify Resource Cleanup

After the CloudFormation stacks have been deleted, verify that all resources have been properly cleaned up:

```bash
# Verify CloudFormation stacks are deleted
aws cloudformation list-stacks --query "StackSummaries[?contains(StackName, 'akuity') || contains(StackName, 'vscode')].{Name:StackName,Status:StackStatus}" --output table

# Verify EKS clusters are deleted
aws eks list-clusters

# Verify EC2 instances are terminated
aws ec2 describe-instances --filters "Name=tag:Name,Values=VSCodeServer" --query "Reservations[].Instances[].{ID:InstanceId,State:State.Name}" --output table
```

## 5. Additional Cleanup (If Needed)

If any resources remain after CloudFormation stack deletion, you may need to manually delete them:

### Check for Lingering CloudWatch Logs

CloudWatch Logs may persist even after stack deletion:

```bash
# List log groups created during the workshop
aws logs describe-log-groups --query "logGroups[?contains(logGroupName, 'akuity') || contains(logGroupName, 'eks') || contains(logGroupName, 'VSCode')].logGroupName" --output table

# Delete any remaining log groups (replace LOG_GROUP_NAME with the actual name)
aws logs delete-log-group --log-group-name LOG_GROUP_NAME
```

## 🎉 Congratulations!

You've successfully cleaned up all resources created during the workshop. This ensures you won't incur any unexpected charges for resources you're no longer using.

If you have any questions or encounter any issues during the cleanup process, please reach out to the workshop facilitators or refer to the [AWS documentation](https://docs.aws.amazon.com/) for additional guidance.
