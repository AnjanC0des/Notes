---
title: "Hi"
output: pdf_document
---

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Work+Sans:wght@500&display=swap" rel="stylesheet">

<style>
div {
    font-family: 'Work Sans', sans-serif;font-size: 16px;
}
</style>
<div>

# AWS Notes
## IAM
#### **Introduction**
* **IAM (Identity and Access Management)** is a **global** service.
* The root account which is created with your Amazon account **cannot** be used to do operations as is. 
* To make it accessible to others and ensure that the account is secure and only necessary previlege is given to people IAM is used.
* We make various users, groups and roles to manage identity and access.
* **Users** are profiles for people.
* These users may or may not belong to **one or more groups**.
* **Groups** are a great way to bunch users together and give a certain set of permissions to everyone in that group.
* We give permissions to users and groups. The json document detailing the permissions are called **policies**.
* We can also give separate permissions to people apart from groups.

Enter iam group slide.

**Creating IAM user and alias:**
* IAM dashboard-> Users(under Access Management)-> 
* Specify user details->
    * Given user name
    * Provide access to AWS management console
    * Select create an IAM user
    * Enter a password
    * Next->
* Set Permissions->
    * Create a group-> Give group name-> Find AdministratorAccess policy and select it-> create user group
    * Select the created group
    * Next->
* Review and create-> create user->
* Return to user List

* In IAM dashboard, in the right pane, edit the Account Alias and use the sign-in url to login.
* You can use the IAM user details to login.

#### **IAM policies**

* User group policies and inline policies stack
Enter iam policy slides

**IAM policies are commonly encountered:**
* Users-> user-> add permissions->
  * Attach existing policies (OR) add group (OR) copy permissions from existing user
* User Groups-> create group -> add users -> attach policies.
* Policies-> Policy -> details like summary and json
* Policies -> create policy
* Remove policies from User permissions.
---  

</div>