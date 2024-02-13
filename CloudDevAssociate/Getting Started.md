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
* google auth, authy(multi device), yubikey(),hardware key fob,ahrdware key for for gov cloud.
* Your should atleast have your root account and admin account have mfa since they manage everything.

#### AWS access keys, CLI and SDK
* We can access our aws account through three ways, through management console, through cli(access keys) and through sdk(app access keys).
* access key id as username and seceret access key as password. Not to be shared with anyone since they can make their own access keys.
* aws cli is the cli to manage all the aws tasks. further-more we can have more functionaly like automation and faster management with cli once mastered.
* We cna also run the aws cli in our browser using cloudshell cli.
* sdk is language specific, embedded in your application to manage aws resources from your app.

#### IAM roles for services
* for services such as ec2,etc to do access aws and do stuff we need to have an iam role attached to it. A service with a iam role attached is considered as one entity.
* common roles:
*  ec2 roles
*  lamda function roles
*  cloudformation roles

#### Audit
* We can check usage and be more effective in access management through iam credential reports and iam access advisor.
* They are part of iam security and access management tools.

### EC2
* EC2(Elastic compute cloud) is one of the main services offered by aws.
* EC2 is used in conjuntion with services such as ebs(elastic block store) to store data, elb(elastic load balancer) to distribute load across various ec2 instances, asg(auto scaling group) to scale the services up or down when needed.
* EC2 instances can be configured as follows:
   * OS : the operating system running on the insatance
   * CPU : the compute power and number of cores used
   * ram
   * storage
     * Network attachedw(ebs/efs) or hardware of ec2 itself
   * Network card- speed and public ip address
   * firewall rules - security groups
   * bootstrap scripts(ec2 user data scripts)- scipts that run when the instances are initialised to set up the instance
* We can access our ec2 instance through ssh if it is configured to accecpt a ssh connection. SSH connection can be done from the terminal but we need the key pair produced during the instance creation.
* We can also access our instance through the ec2 instance connect from the ec2 instances page. Security groups must be configured to accecpt ssh connection for this to work.
* We can also attach roles to ec2 instances from the instances page.
* We can also choose how we are billed for ec2 instances. Different payment plans are as follows:
   * On-demand: This is the base price of the instances with 0% discount and we are billed per second. We pay as we use. This is best when we dont know which instances we are using and we are using the service for a short period of time.
   * Reserved instances: Instances can be reserved for 1 or 3 years. We also have a choice for reserved instances and reserved and convertible instances. This is best when we know we have a great workload and we reserve instances for 1 or 3 years. 72% discount.
   * Savings plan : We commit to duration of usage 1 or 3 years and we use this when we know of the duration of usage but not the type of instances we would be using. We lock in on a certain instance family and aws region. 72% discount.
   * Spot instances: These are piss cheap instances that we can loose at any time if someone else bids a higher price for them and are suitable for jobs that are not affected by instances shutting off randomly. 90% discount.
   * Dedicated hosts : We get a whole physical host to ourselves and this is used when we need more low level access or when our billability/licensing is associated with dedicated host. Purchasing options can be on demand or reserved(1 or 3 years). This is the most expensive option. Reservation on dedicated hosts can gice us upto 70% discounts.
   * Dedicated instances : Other hosts wont share our harware.
   * Reserved instances : We reserve instances in a certain az and pay for them even if we dont use them. No time commitments and billing discounts.

### EBS

 



