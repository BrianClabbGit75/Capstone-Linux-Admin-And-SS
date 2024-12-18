# Capstone-Linux-Admin-And-SS
Shell Scripting for CloudOps, including IAM, users, groups, permissions etc


This is a script for fictitious company called CloudOps Solutions, using AWS Cloud, we will automate the process of managing IAM including creation of users, groups, and assignment of permissions to DevOps team - please see folllowing script with explanation

Steps:

•	Create IAM Users: generate unique usernames and passwords for each DevOps team member

•	Create IAM Groups: Define groups like e.g "DevOps Engineers" and "DevOps Managers" to organise users based on their roles.

•	Assign Permissions to Groups: Attach specific IAM policies to these groups, granting them necessary permissions to perform their tasks (e.g., EC2 access, S3 access).


This will be performed using AWS CLI

```markdown
Bash
#!/bin/bash

# Function to create an IAM user
create_user() {
  user_name="$1"
  user_password="$2"

  aws iam create-user --user-name "$user_name"
  aws iam create-access-key --user-name "$user_name"
  aws iam create-login-profile --user-name "$user_name" --password "$user_password"
}

# Function to create an IAM group
create_group() {
  group_name="$1"

  aws iam create-group --group-name "$group_name"
}

# Function to add users to a group
add_user_to_group() {
  user_name="$1"
  group_name="$2"

  aws iam add-user-to-group --user-name "$user_name" --group-name "$group_name"
}

# Function to attach a policy to a group
attach_policy_to_group() {
  group_name="$1"
  policy_arn="$2"

  aws iam attach-group-policy --group-name "$group_name" --policy-arn "$policy_arn"
}

# Example usage:

# Create DevOps Engineers group
create_group "DevOpsEngineers"

# Create DevOps Managers group
create_group "DevOpsManagers"

# Create users and add them to groups
create_user "user1" "password123"
add_user_to_group "user1" "DevOpsEngineers"

create_user "user2" "password456"
add_user_to_group "user2" "DevOpsManagers"

# Attach policies to groups
attach_policy_to_group "DevOpsEngineers" "arn:aws:iam::aws:policy/AmazonEC2FullAccess"
attach_policy_to_group "DevOpsManagers"
"arn:aws:iam::aws:policy/AdministratorAccess"

```

<ins>Explanation of Code</ins>


•	Functions: The script defines functions for creating users, groups, adding users to groups, and attaching policies to groups.   

•	User Creation: For each user, we create a username, password, and access key.   

•	Group Creation: We create groups like "DevOpsEngineers" and "DevOpsManagers."   

•	User Assignment: We add users to their respective groups.   

•	Policy Attachment: We attach appropriate IAM policies to the groups.



