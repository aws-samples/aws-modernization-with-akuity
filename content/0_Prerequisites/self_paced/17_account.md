---
title: "Setting up your Workshop Resources"
chapter: false
weight: 17
---

{{% notice warning %}}
Your account must have the ability to have Administrative Access
{{% /notice %}}

# Deploying the CloudFormation Templates  

To set up the required resources for this workshop, you will need to deploy two CloudFormation templates:  

1. :button[Download vscode-server.yaml]{href="/static/infrastructure/vs-code-server.yaml" action=download}

2. :button[Download eks-cluster.yaml]{href="/static/infrastructure/eks-cluster.yaml" action=download}

---

## Prerequisites  

Before deploying the templates, ensure the following:  

- **AWS account:** Must have an AWS Account [Click Here to Register for an Account](https://aws.amazon.com/free/?gclid=CjwKCAiApY-7BhBjEiwAQMrrEQvPVHrROjm_VPCmPQKxuQ5MDb45z8R8_aYf9qnh9YTa2K88EwxLoRoCZcoQAvD_BwE&trk=78b916d7-7c94-4cab-98d9-0ce5e648dd5f≻_channel=ps&ef_id=CjwKCAiApY-7BhBjEiwAQMrrEQvPVHrROjm_VPCmPQKxuQ5MDb45z8R8_aYf9qnh9YTa2K88EwxLoRoCZcoQAvD_BwE:G:s&s_kwcid=AL!4422!3!432339156165!e!!g!!aws%20account!9572385111!102212379047&all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc&awsf.Free%20Tier%20Types=*all&awsf.Free%20Tier%20Categories=*all)
- **Administrator Access**: Verify that you have administrative permissions in your AWS account.  
- **AWS Management Console**: Log in to the [AWS Management Console](https://aws.amazon.com/console/).  

---

## Deploying the Templates  

### Step 1: Deploy the `vscode-server.yaml`  

1. Navigate to the **CloudFormation** service in the [AWS Management Console](https://aws.amazon.com/console/).  
2. Click **Create stack** and select **Upload a template file**.

   ![Create Stack Button](/images/cloudformation-create-stack.png)  

3. Click **Choose file**, select the `vscode-server.yaml`, and click **Next**.  

   ![Upload Template](/images/cloudformation-upload-template.png)  

4. Enter a **Stack Name** (e.g., `vscode-server`).  
5. Review and modify the parameters as needed. Leave default values unless instructed otherwise.  

   ![Stack Parameters](/images/vscode-server-parameters.png)

6. Click **Next**, then review the stack details.  
7. Acknowledge the **IAM role creation** if prompted by checking the appropriate box.  

   ![Acknowledge IAM Roles](/images/cloudformation-acknowledge-iam.png)  

8. Click **Submit** to start the deployment.  

   ![Create Stack Process](/images/cloudformation-create-process.png)

---

### Step 2: Deploy the `eks-cluster.yaml`

1. Repeat the same steps as above, but upload the `eks-cluster.yaml` file.  
2. Enter a **Stack Name**(e.g., `akuity-aws-cluster`) and do not modify any **Parameters**.  
3. Proceed with the deployment.

   ![VS Code Parameters](/images/cloudformation-stack-parameters.png)  

---

## Verifying the Deployments  

- Go to the **CloudFormation Outputs** tab for each stack to verify the deployment details.  

   ![CloudFormation Outputs Tab](/images/cloudformation-outputs.png) 

- The `vscode-server.yaml` stack will provide the `VSCODEURL` and `Password` for accessing the VS Code server.

Once the stack status changes to `CREATE_COMPLETE`, the resources for the Akuity x AWS Workshop are ready.  

---

**Note**: If you encounter errors during the deployment, ensure that:  
1. You have sufficient permissions to deploy CloudFormation stacks.  
2. Your AWS account has the required service limits for the resources being deployed.  
3. All parameters are correctly configured as per the workshop requirements.  

If you have any issues, refer to the troubleshooting section or contact the support team.
