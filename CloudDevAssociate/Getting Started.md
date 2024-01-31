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
**Regions**: regions all around the world, has names such 
cluster of data centers
most services are region scoped
how to choose a aws region? 
Depends on some factors such as 
compliance : data governance and legal req
proximity
pricing
availability 
**Availability Zones**: region has 3 to 6 availability zones
each az has discrete data centers with redundant power networking and connectivity
separate and isolated from disaster
connected to other azs with high bandwidth ultra low latency networking to make a region
**Data centers**
**Edge location/points of presence** more than 400 pop

example of global services: 
iam dns
cloudfront 
web application firewall

example of regional services:
ec2 elastic beanstalk lambda

### IAM
identity and access management
root account shouldnt be used or shared
users are created and grouped
users can belong to none or mutiple groups

users are created and assigned permissions
users and groups are assigned permissions called policies.
policies define permissions
least previlege principle: dont give more permission than a suer needs

#### iam policies inheritance
policies attacehd at group level- policy applied to all group members

user without a group can have inline policies
users that are multiple groups inherit their policies
consists of:
version
id
statement: has a sid, effect(allows or denies access),principal(account user role to which this policy is applied to), action(list of action this policy allows or denies), resource list(list of resources where the actions are applied), condition(conditions when the policy comes into effect)




