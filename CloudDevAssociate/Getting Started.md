# AWS DVA C02 certification(developer associate)
**What is AWS?**
* Cloud provider which provides servers and services on demand and scale easily.
* It contains a plethora of services and tools that work in tandem to make software solutions more robust and scalable.
* It not only ensures performance but a majority of aws tools and services are pay as you use and hence are cost efficient and prevent hardware costs.

### Signing up for AWS
* We need a root email address which will be used for verification, recovery and administrative functions.
* We need to provide an account name for ourselves.
* We need to verify the email address provided.
* We will provide a root user password and confirm it. This password can be recovered from email but forgetting it is not preferred.
* Mention type of account(Course chose personal) and then provide additonal details for this account.
* Then we need to enter credit card information.
* Verify your identity and with phone number and sms or call and select a support plan. Sign up process is complete.
* We then go to aws management console and we can sign in with root user email and password.

### AWS Global infrastructure
**Regions**: 
* Ther are various regions all around the world 
* They are clusters of data centers.
* Most services are region scoped, i.e., their effectivity is restriced to the region in which they are spun/used.
* **How to choose a aws region for somrthing like say deploying an app?**
Depends on some factors such as :
  * compliance : data governance and legal restriction based on region.
  * proximity : region of close proximity has low latency
  * pricing : pricing can vary with regions
  * availability : some services and resources may or may not be available in some region.
**Availability Zones**:
* Each region has 3 to 6 availability zones.
* Each AZ has multiple discrete data centers with redundant power, networking and connectivity.
* They are kept separate and isolated from disaster.
* They are connected to other AZs with high bandwidth ultra low latency networking to make a region.
**Data centers** : They are physical locations that consist of computing machines and their related hardware.
**Edge location/points of presence** : There are more than 400 pop worldwide. Each pop is isolated, so failure to one pop wont affect the global network.

Some examples of global services: iam, dns, cloudfront, web application firewall
example of regional services: ec2, elastic beanstalk, lambda

### IAM
* It manages identity and access management for your AWS account.
* The root account shouldnt be used or shared in general for security purposes.
* In IAM users are created and grouped so that they can be more easily managed.
* Users can belong to none or mutiple groups.
* Users are created and assigned permissions called policies and these are either assigned directly(inline) or inherited from groups.
* Best practice is to use **least privilege principle** : dont give more permission than a user needs.

#### iam policies inheritance
* When policies attached at group level it is applied to all group members.
* Users without a group can have inline policies.
* Users that are in multiple groups inherit their policies.
* A policy consists of:
  * version
  * id
  * statement:
    * has a sid(statement id)
    * effect(allows or denies access)
    * principal(account user role to which this policy is applied to)
    * action(list of action this policy allows or denies)
    * resource list(list of resources where the actions are applied)
    * condition(conditions when the policy comes into effect)
 
#### MFA
* passwords you know+device you know
* google auth, authy(multi device), yubikey(),hardware key fob,ahrdware key for for gov cloud




