# AWS IAM Management Script

## Introduction
**Overview:** This project focuses on developing an automated shell script to manage AWS Identity and Access Management (IAM) resources using the AWS Command Line Interface (CLI). The script automates the creation of IAM users, IAM groups, and the attachment of an administrative policy. This process is essential for efficiently onboarding new employees and ensuring secure access to AWS resources.

## Objective: 

The primary objective of this project is to:

- Create IAM users for five new employees.
- Create an admin IAM group.
- Attach the AWS-managed policy AdministratorAccess to the group.
- Assign the users to the admin group, thereby granting them administrative permissions.

This document details the script development process, including environment setup, script functionality, testing procedures, and how to execute the script.

## Environment Setup

Before running the script, certain prerequisites must be met to ensure proper execution and testing.

**AWS CLI Installation and Configuration**

To interact with AWS services from the command line, you need to install and configure the AWS CLI. Follow the steps below to set it up:

1. **Install the AWS CLI:**

    - The AWS CLI can be installed on various operating systems (Windows, macOS, Linux). Follow the AWS documentation for your system: **AWS CLI Installation Guide.**

2. **Configure the AWS CLI:**

    - After installation, configure the AWS CLI with your AWS credentials and default region. Use the following command to set up: `aws configure`

    - Provide the following information:
        - AWS Access Key ID: Your access key for the IAM user.
        - AWS Secret Access Key: The secret access key for your IAM user
        - Default region name: The region where the resources will be created (e.g., us-east-1).
        - Default output format: Usually set to json or text.

        ![](./img/1.configure-AWS-CLI-on-local-machine.png)

3. **Ensure Required Permissions:**

    - The IAM user running the script must have permissions to manage IAM resources (users, groups, and policies). Assign the AdministratorAccess policy to the user, or ensure the user has permissions to execute the following actions:

        - iam:CreateUser
        - iam:CreateGroup
        - iam:AttachGroupPolicy
        - iam:AddUserToGroup
    
    ![](./img/9.add-administrator_access-to-automation_user.png)

4. Verify AWS CLI Connectivity

    ![](./img/0.Verify-AWS-CLI-Connectivity.png)

    This will return your account ID and IAM user or role information. Verify that this is the correct AWS account where you expect to see the users.

## aws_cloud_manager.sh - Shell Script

**Objective:** Write script to automate the creation and management of IAM resources for five new employees.

1. **Define IAM User Array**

    - In your script, you will define an array of IAM usernames for easy iteration when creating users.

    ![](./img/1.create-script-file.png)
    ![](./img/2.define-iam-user-array.png)

2. **Function to Create IAM Users**

    - The aws iam create-user command will be used to create IAM users. This is where you'll loop through the IAM_USERS array and create users.

    ![](./img/3.function-to-create-iam-users.png)

3. **Create IAM Group**

    - Use the aws iam create-group command to create an IAM group named admin.

    ![](./img/4.function-to-create-iam-group.png)

4. **Attach Administrative Policy to Group**

    - To give the group administrative privileges, use the aws iam attach-group-policy command with the AdministratorAccess policy.

    ![](./img/5.attach-policy-to-iam-group.png)

5. **Assign IAM Users to Group**
    - To assign the created IAM users to the admin group, use the aws iam add-user-to-group command in a loop.

    ![](./img/6.assign-users-to-iam-group.png)

6. **Execute functions in sequence**

    ![](./img/7.execute-function-in-sequence.png)

7. Running the Script

    - You can run the script from your terminal using Git Bash or directly in any shell-supported environment: `./aws_cloud_manager.sh`

    **OUTPUT:**
    ![](./img/10.run-scipt.png)

    ![](./img/11.run-script2.png)

    ![](./img/12.run-script3.png)

8. Testing and Verification

    - Check the IAM users in the AWS Management Console or by using: `aws iam list-users`

    **By using `aws iam list-users`:**
    ![](./img/15.list-users.png)


    **By using AWS Management Console:**

    ![](./img/13.list-of-users.png)

    ![](./img/14.user-group.png)

## Conclusion

This script leverages the AWS CLI to automate the management of IAM resources. It helps efficiently onboard new users, assign them to an administrative group, and apply policies, all through a shell script.
