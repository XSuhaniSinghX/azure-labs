# 📘 Azure Lab Assignment – Full Documentation

This file documents all steps, commands, and screenshots used for the Azure lab assignment tasks.

---

## ✅ Task 1: Azure Identity, Roles & Access Control

### 🔹 Objective

* Observe Azure subscription and Entra ID
* Create test users and groups
* Assign built-in and custom RBAC roles

### 🔧 Steps

#### 1. View Subscription and User Info

```bash
az login
az account show --output table
az ad signed-in-user show --output table
```

📸 Screenshot: ![Subscription Info](screenshots/subscription_info.png)

#### 2. Create User and Group

```bash
az ad user create --display-name "TestUser" --user-principal-name testuser01@XBEELZEBUB666Xoutlook.onmicrosoft.com --password "P@ssw0rd123!"
az ad group create --display-name "TestGroup" --mail-nickname "TestGroup"
az ad user list --output json > users.json
```

📸 Screenshot: ![User and Group Created](screenshots/user_group_created.png)

#### 3. Get User Object ID and Add to Group

Extracted ID from JSON: `e210c3b4-fa59-48d7-b8d9-b3ddbcbfb586`

```bash
az ad group member add --group "TestGroup" --member-id e210c3b4-fa59-48d7-b8d9-b3ddbcbfb586
```

#### 4. Assign Built-in RBAC Role

```bash
az role assignment create --assignee testuser01@XBEELZEBUB666Xoutlook.onmicrosoft.com --role Reader --scope /subscriptions/<your-subscription-id>
```

📸 Screenshot: ![Built-in Role Assigned](screenshots/reader_role_assigned.png)

#### 5. Create and Assign Custom Role

**customRole.json:**

```json
{
  "Name": "CustomReader",
  "IsCustom": true,
  "Description": "Read-only access to RGs",
  "Actions": [
    "Microsoft.Resources/subscriptions/resourceGroups/read"
  ],
  "AssignableScopes": [
    "/subscriptions/<your-subscription-id>"
  ]
}
```

```bash
az role definition create --role-definition customRole.json
az role assignment create --assignee testuser01@XBEELZEBUB666Xoutlook.onmicrosoft.com --role "CustomReader" --scope /subscriptions/<your-subscription-id>
```

📸 Screenshot: ![Custom Role Assigned](screenshots/custom_role_assigned.png)

### ✅ Task 1 Complete

---



