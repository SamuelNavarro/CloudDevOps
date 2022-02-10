# Cloud Fundamentals


## Jobs in Cloud Computing ##
### Cloud Developer ###

**Job Duties:**

- Designing and developing secure, scalable cloud applications, and products.
- Assisting in developing automated tooling for deployment and maintenance.
- Defining and documenting best practices and strategies regarding application deployment and infrastructure maintenance.

**Required Skills:**
- Programming Languages (e.g., Python)
- Web Services & API
- Networking, Storage, Compute, Security on Cloud
- Deploying Software in Cloud
- Web Development (i.e. HTML, CSS)
- Virtualization & Containers

### Cloud DevOps Engineer ###

Job Duties:

- Building and scaling services in a cloud.
- Configuration management.
_ Building automated systems/infrastructure, and develop pipelines to make remote updates to software eliminating any effort for users.

Required Skills:
- Programming Language (i.e. Python)
- Infrastructure as Code
- CI/CD Tools (Jenkins)
- Monitor Software & Infrastructure
- Orchestration (i.e. Kubernetes)
- Infrastructure Automation (i.e. Ansible)

### Cloud Solutions Architect ###

Job Duties:

- Delivering solution architecture to engineering teams, communicating their value to ensure good implementation.
- Offering guidance in infrastructure movement techniques, such as bulk application transfers into the Cloud (lift or shift, or adopting cloud-native approach).
- Driving experiments to evaluate new technologies and methodologies to accelerate project delivery.

Required Skills:

- OS Concepts (e.g. Linux)
- Networking, Storage & Security Fundamentals
- Application and Infrastructure Architecture & Design principles
- Automation & Orchestration
- IT Governance




## Foundational & Compute Service ##


### EC2: Elastic Cloud Compute ###

EC2 is not considered serverless. 

There are several pricing options for EC2.

- On Demand - Pay as you go, no contract.
- Dedicated Hosts - You have your own dedicated hardware and don't share it with others.
- Spot - You place a bid on an instance price. If there is extra capacity that falls below your bid, an EC2 instance is provisioned. If the price goes above your bid while the instance is running, the instance is terminated.
- Reserved Instances - You earn huge discounts if you pay up front and sign a 1-year or 3-year contract.


Instances

The simplest form of the EC2 Instance is the pay as you go, the on-demand instance, and that's this type of instance created using the default Launch wizard available on the EC2 dashboard. It's just the normal one pay as you go.

- Instances - It shows the list and details of the instances running in a given region.
- Instance Types - It shows the list of instance types (different combinations of hardware - CPU, storage, memory, architecture) available to launch a new instance.
- Launch Templates - These are the scripts that contain configuration information written either in JSON or YAML format to automate instance launches, simplify permission policies, and enforce best practices across your organization.
- Spot Requests - Spot is where you actually bid on an instance. If the price falls below your bid, the instance is automatically spun up and if the price goes above your bid, the server is automatically terminated. So this is good if you have an application that has a flexible start and stop time.
- Reserved Instances - This is where you sign a contract for your EC2 Instance in either one to three years and you get a huge discount. So, this is good when you know the steady-state for your applications and you want to pay upfront.
- Dedicated Hosts - This is where you have your own dedicated hardware. You may have license requirements for certain software packages that say no multi-tenancy. Meaning that you cannot run that application on a shared server. So Dedicated Hosts would solve that problem.
- Capacity Reservations - This allows you to reserve the desired capacity (count) of instances in a particular availability zone. The reserved capacity is charged at the selected instance type’s On-Demand rate whether an instance is running in it or not.

- See the detailed summary of all types and purchasing options here [here](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-purchasing-options.html)

**Images**

- AWS provides an option to create custom AMIs. Alternatively, you can use Images owned by Amazon and others. The AMI dashboard shows the Images owned by you. You can build a custom Image by using the EC2 Image Builder wizard available on this dashboard.
**Elastic Block Store (EBS)**
In simple words, you can think of EBS as an external hard drive that we attach to the server for additional storage.

**Volumes** - It shows the list and details of all the volumes currently available to use. You can re-purpose a volume, meaning, you can anytime attach or detach a volume to any instance. You can create new volumes by using the Create Volume wizard. AWS provides the option to have a variety of volumes, such as general-purpose solid-state drive (SSD), provisioned SSD, general hard-disk (HDD), throughput-optimized HDD, or magnetic drives. Each type of volume has a different serving capacity, such as the number of I/O operations per second.
**Snapshots** - A snapshot is the saved state of the data in the (existing) volume at a particular moment. Snapshots can be used to transfer volumes from one instance to another or saving the state for future use.
**Lifecycle Manager** - It helps to schedule and manage the creation and deletion of EBS snapshots.

**Network & Security**
- Security Groups - A security group acts as firewall rules that control the traffic for EC2 instances or virtual private clouds (VPC). You can define multiple security groups. A given security group can be assigned to multiple EC2 instances.

When you launch an instance, you can specify one or more security groups. You can modify the rules for a security group at any time; the new rules are automatically applied to all instances that are associated with the security group.

- Elastic IP addresses - An Elastic IP address is a static IPv4 address. Assume you have a server running on an EC2 instance, that has a specific IP address. In case, the instance fails, the back-up instance will spin up. The back-up instance will have a different IP address, which will require you to update the IP address used in your client application. This problem can be solved by using the elastic IP address. An Elastic IP address can mask the failure of an instance by remapping the current IP address to another instance in your account.
- Placement Group - You can imagine the EC2 instances as VMs running on the real servers in a data center. By default, the EC2 instances that you launch will be spread out across underlying hardware. But, sometimes there is a requirement to place the group of interdependent instances to meet the needs of your workload. AWS allows to place the instances based on either of the following placement strategies - cluster (tightly packed), partition (logically grouped), or spread evenly across the underlying hardware.
- Key Pairs - A key-pair is pair of (encrypted) public and (unencrypted PEM encoded) private keys. The public key is placed automatically on the instance, and the private key is made available to the user, just once. You can only log in to your running instance with the help of your private key.
- Network Interfaces - A network interface represents a virtual network card in a VPC, and it has a both private and public IP addresses. When you create an instance, a default network interface is attached to it. In this dashboard, you can create and attach additional network interfaces to any instance. An EC2 instance can have multiple network interfaces.

**Load Balancing**
- Load Balancer - A load balancer distributes the incoming traffic across multiple targets, such as EC2 instances in one or more Availability Zones. AWS supports three types of load balancers: Application Load Balancers, Network Load Balancers (new), and Classic Load Balancers (might become deprecated soon).

**EC2 Auto Scaling**
- It is a service that automatically launches/terminates EC2 instances based on user-defined scaling policies, scheduled actions, and health checks. It ensures that you have a specified number of instances always up and running. You can specify the minimum and maximum count of instances. This service uses launch templates, i.e., a script containing the configuration details of the instances that will be launched automatically.




### Connect to Linux Instance ###


Recently, AWS has launched the EC2 Instance Connect wizard, which can help you to connect directly from the EC2 dashboard. Alternatively, you can use SSH as well.


We need to first:
`chmod 400 <path to .pem>`

Then connecto to its public DNS as: 
`ssh -i "AWS_EC2_Demo.pem" ec2-user@ec2-52-200-123-86.compute-1.amazonaws.com:w`



### EBS ###


Two types of memory for an EC2 instance. In-memory and EBS. The benefit of EBS over in memory is that you be able to persist data after EC2 is terminated. And that EBS is automatically replicated in AZ. 

### VPC ###

**Flat Network** all devices and workstations are connected to a single switch. Meaning that all devices are part of the same broadcast network where they can communicate with each other. **VPC** allows you to create your own private space or private network in the cloud. 

You can launch services, like EC2, inside of that private network. A VPC spans all the Availability Zones in the region.

VPC allows you to control your virtual networking environment, which includes:

- IP address ranges
- subnets
- route tables
- network gateways

**Tips**
VPC is found under Networking & Content Delivery section of the AWS Management Console.
The default limit is 5 VPCs per Region. You can request an increase for these limits.
Your AWS resources are automatically provisioned in a default VPC.
There are no additional charges for creating and using the VPC.
You can store data in Amazon S3 and restrict access so that it’s only accessible from instances in your VPC.


Services under VPC

In the navigation on your left, you can see a categorized list of services that become a part of a VPC. Let's have an overview of a few key concepts:

- **Your VPCs** - It will list all your VPCs and display the deep-dive details of the selected VPC. Each VPC has a valid IPv4/IPv6 CIDR block allocated to it. Every resource in the VPC will have an IP address from the allocated CIDR block. Though, a few IP addresses reserved for special purposes.
- **Subnets** - It represents a subset of your VPC, i.e., a range of IP addresses from the CIDR block allocated to your VPC. Subnets of a VPC can be present in different AZs.
- **Route tables** - These are the set of rules, called routes, that determine to which IP address the network traffic should be directed.
- **Internet gateways** - If any of your resources within your VPC wants to communicate to the internet, then you must attach an internet gateway to your VPC. The internet gateway enables the communication between resources in your VPC and the internet.

### Create VPC ###


When creating the vpc:
The VPC configuration includes:

- The IP address in the VPC follows a classless inter-domain routing (CIDR) block of IP addresses. You will have to specify the IPv4/IPv6 CIDR block to be allocated to the VPC. In the snapshot above, it uses an IPv4 `10.0.0.0/16` block, which allocates `2^(32-16) = 65,536` IP addresses. A few IP addresses are reserved, so you get `65531` IP addresses for further allocation.
- You will have to specify the range of IP address from the allocated CIDR block for each subnet. In the example above, the public subnet has been allotted the `10.0.0.0/24` range, which comprises `2^(32-24) = 256` IP addresses. But, again a few IP addresses are reserved, so you get `251` available for resources in that subnet.
- Similarly, for the private subnet in the snapshot above, you will get 251 IP addresses.
- Specify the AZ for each subnet, NAT gateway or elastic IP allocation ID, and the service endpoints that will allow you to privately connect your VPC to supported AWS services.


### VPC: Network ACL ###

A network access control list (ACL) defines the set of firewall rules for controlling traffic coming in and out of subnets in your VPC.

You can view the Network ACLs under the Security section in the left navigation pane of the VPC Dashboard.


1. List of Network ACLs
For each Network ACL in the list, view the ID, the count of associated subnets, whether it is a Default, the VPC Id to whom the network ACL is associated, and the owner ID.

2. Details of the Selected Network ACL
View the details of the selected Network ACL. In the snapshot above, it shows the details of a default Network ACL. Note that each VPC automatically gets associated with a modifiable default network ACL. Each subnet in your VPC must be associated with any one network ACL. Whereas, a given network ACL can be associated with multiple subnets.

**Inbound/Outbound Rules**
- The default network ACL allows all inbound and outbound IPv4 traffic, as shown in the snapshot above. However, you can create or edit the rules, anytime.
- Inbound/Outbound rules are numbered and ordered. The lowest numbered rule is evaluated first. In other words, the incoming/outgoing traffic to/from a given subnet follows the rules mentioned in the associated network ACL.
- Network ACLs are stateless in nature. Assume an inbound request arrived in your subnet. A "response" to the inbound request can only be sent out of the subnet if the outbound rules allow the outgoing traffic to the desired destination. A vice-versa scenario is also possible.


### Lambda ###

- Compute power in the cloud
- Chunk of code
- One specific task
- Lambdas have a time limit of 15 minutes.
- The code you run on AWS Lambda is called a “Lambda function.”
- Lambda code can be triggered by other AWS services.
- AWS Lambda supports Java, Go, PowerShell, Node.js, C#/.NET, Python, and Ruby. There is a Runtime API that allows you to use other programming languages to author your functions.
- Lambda code can be authored via the console.
- Is event-driven. Can run code on certain events happening. 



**Step 0. Prerequisite: Create an S3 bucket**
AWS S3 is a file storage service. Though, we will learn S3 in detail in the upcoming lesson, let's create an S3 bucket (folder) for this exercise.

Go to the S3 dashboard, and click on the Create bucket.
![lambda1](./images/lambda1.png)


Enter the bucket name, and make it visible to the public. The name should be unique worldwide, you can use the convention as `my-<aws account id>-bucket`. Leave other fields as default, and create the bucket.


![lambda2](./images/lambda2.png)
![lambda3](./images/lambda3.png)

**Step 1. Create a Lambda Function**
From the AWS Management Console page, select the Lambda service.
Use the Create function wizard, and select the Author from scratch option.
Use the following basic information to create a function:

> Function name and rutime python 3.8

**Step 2: Add a Trigger**
Next, the wizard will automatically display the details of the newly created function. Add a trigger under the Designer section

Click Add Trigger
![lambda4](./images/lambda4.png)


- On the Add Trigger screen, select “S3” as the trigger
- Select the S3 bucket name for the Bucket
- For Event Type, select “All object create events”.
> This means that anytime a file is created (or uploaded) to the selected S3 bucket, the lambda function will be triggered
- Acknowledge the Recursive invocation message 
- Click the Add button . Congratulations, you’ve added a trigger!
In the Designer section, click on the name of the Lambda to have the Function Code section reappear

**Step 3. Configure Test event**
Next, the wizard will automatically display the details of the newly created function.

- Click on the Test button on the upper right-hand corner, to configure test event(s).
- Ensure the Event template is Hello World.
- For the Event name enter TestEvent.
- Update the JSON to the statement below, replacing the string value with your name.

**Step 4: Modify Lambda Function**

Modify it and deploy your saved function by clicking on the **Deploy** button


**Step 5. Test a Lambda Function**
Click the Test button in the upper right-hand corner again to test your function.
The output will be displayed in the Execution results section at the top. Expand the Details to review the output.
![lambda5](./images/lambda5.png)


**Step 6. Add files to the bucket**

From the S3 dashboard, click on the name of the bucket you have created in the first step above.
![lambda6](./images/lambda6.png)

- Upload a few files to the bucket, from your local computer.
![lambda7](./images/lambda7.png)
![lambda8](./images/lambda8.png)

**Step 7. Check if the Lambda function is triggered**
Go back to the Lambda console, and select your function to view its details.
Click on the Monitoring tab to view the metrics that show the number of times the Lambda function is triggered as a response to file(s) upload in the S3 bucket.


![lambda9](./images/lambda9.png)

You can view the detailed Invocations chart in the CloudWatch console.

![lambda10](./images/lambda10.png)

The detailed graph in the CloudWatch console shows that the Lambda function was triggered thrice. See the snapshot below.

![lambda11](./images/lambda11.png)
**Step 8. Delete resources**
Do not forget to delete the Lambda function, and the S3 bucket after the exercise is over.
To delete the Lambda function, go back to the Lambda console, select the checkbox against the function name, and choose the delete action.

![lambda12](./images/lambda12.png)

To delete the S3 bucket, go back to the S3 console, select the bucket checkbox against the bucket name, and empty and then delete the bucket.
![lambda13](./images/lambda13.png)


### Elastic Beanstalk ###


Can launch VPC, EC2 Instance, Elastic Load Balancer.



## Storage & Content ##

### S3 ###

Details of an Existing Bucket
**1. Properties**
There are several properties that you can set for S3 buckets, such as:

Bucket Versioning - Allows you to keep multiple versions of an object in the same bucket.
Static website hosting - Mark if the bucket is used to host a website. S3 is a very cost-effective and cheap solution for serving up static web content.
Requester pays - Make the requester pays for requests and data transfer costs.
Server access logging - Log requests for access to your bucket.
Permissions
It shows who has access to the S3 bucket, and who has access to the data within the bucket. In the example snapshots above, the bucket is public, meaning anyone can access it. Here, we can write an access policy (in JSON format) to provides access to the objects stored in the bucket.

**2. Metrics**
View the metrics for usage, request, and data transfer activity within your bucket, such as, total bucket size, total number of objects, and storage class analysis.

**3. Management**
It allows you to create life cycle rules to help manage your objects. It includes rules such as transitioning objects to another storage class, archiving them, or deleting them after a specified period of time.

**4. Access points**
Here, you can create access endpoints for sharing the bucket at scale. Using an endpoint, you can perform all regular operations on the bucket.

### Dynamo DB ###

DynamoDB is a NoSQL document database service that is fully managed. Unlike traditional databases, NoSQL databases, are schema-less. Schema-less simply means that the database doesn't contain a fixed (or rigid) data structure.

Tips
- DynamoDB is found under the Database section on the AWS Management Console.
- DynamoDB can handle more than 10 trillion requests per day.
- DynamoDB is serverless as there are no servers to provision, patch, or manage.
- DynamoDB supports key-value and document data models.
- DynamoDB synchronously replicates data across three AZs in an AWS Region.
- DynamoDB supports GET/PUT operations using a primary key.


In the shared responsibility model, when working with DynamoDB, what is NOT your responsibility? Pick two.
- Patch or upgrade the database
- Provision or manage servers



### DynamoDB - Create a Table ###


**Create table with the provided tutorial.**

1. Create Item

Data can be added in the form of an item.

> You can imagine an item as analogous to a row in a relational table for simplicity.

Every item consists of one or more attributes. Each attribute consists of a name, a data type, and a value. One of the attributes serves as the primary key. See a sample item entry below.


![Dynamo](./images/DynamoDB1.png)
![Dynamo2](./images/DynamoDB2.png)


2. Details of an Existing Table

There are several useful features provided to help you manage your data found in DynamoDB. For the selected table, you can view the following information in separate tabs:

- Overview - This tab shows high-level details about the table. For example, the table name, partition key, primary sort key (if any), encryption type, and much more. Tables can be encrypted at rest with no overhead. You can also see the region and the Amazon Resource Name (ARN), which is a unique identifier for the current resource.
- Items - It lists all of the items/data stored in the table.
Metrics - View the metrics for your table, such as, read/write capacity (units/sec), count of throttled read/write requests, and count of throttled read/write counts.
- Alarms - Set up alarms to notify you if you exceed your capacity limits. For each alarm, you will have to specify a metric and the upper threshold.
- Capacity - Set up the capacity of the selected table to read and write.
- Indexes - Set up the index using a primary key, and project on a set of attributes. Indexes help you to improve querying performance.
- Global Tables - When you set up a table as a global table, that table can exist in two or more AWS regions with automatic replication.
- Backups - A backup helps in restoring a Point-in-time state. DynamoDB maintains continuous backups of your table for the last 35 days.
- Triggers - Create triggers, for example, you can have a lambda function run whenever data is inserted into the current table.
- Access control - Set up access control policies (JSON files) that can allow access to the current table from Facebook, Google, or Amazon (not AWS).

External Resource
AWS has a very useful tutorial [tutorial](https://aws.amazon.com/getting-started/hands-on/create-nosql-table/) to get started with DynamoDB. It has the following guided sections:

- Step 1: Create a NoSQL Table
- Step 2: Add Data to the NoSQL Table
- Step 3: Query the NoSQL Table
- Step 4: Delete an Existing Item
- Step 5: Delete a NoSQL Table



### RDS ###


RDS doesn't provide accessing to your database via secure shell (SSH).


### RedShift ###


Redshift is a cloud data warehousing service to help companies manage big data. Redshift allows you to run fast queries against your data using SQL, ETL, and BI tools. Redshift stores data in a column format to aid in fast querying.



### Cloud Front ###
A Content Delivery Network (or CDN) speeds up delivery of your static and dynamic web content by caching content in an Edge Location close to your user base.

Benefits
The benefits of a CDN includes:
low latency
decreased server load
better user experience



When a user request your website, the request goes to the **Edge location** first, if the content is not there, the content will be pulled form the origin (which may be far away from your user). 
You can configure for how long a content remains cached and you can manually expire or remove content.

CloudFront is used as a global content delivery network (CDN). Cloud Front speeds up the delivery of your content through Amazon's worldwide network of mini-data centers called Edge Locations.

CloudFront works with other AWS services, as shown below, as an origin source for your application:

Amazon S3
Elastic Load Balancing
Amazon EC2
Lambda@Edge
AWS Shield
Tips
CloudFront is found under the Networking & Content Delivery section on the AWS Management Console.
Amazon countinously adds new Edge Locations.
CloudFront ensures that end-user requests are served from the closest edge location.
CloudFront works with non-AWS origin sources.
You can use GeoIP blocking to serve content (or not serve content) to specific countries.
Cache control headers determine how frequently CloudFront needs to check the origin for an updated version your file.
The maximum size of a single file that can be delivered through Amazon CloudFront is 20 GB.



**Restrictions** is a neat feature, you can prevent IP adreesses from some countries to access your web page.
**Invalidation** button is to delete cache outside the schedule. 


### S3 and CloudFront ###

In this hands-on exercise, you will access private S3 bucket content via a Cloud Front distribution. You will also learn that CloudFront, after caching, speeds up the delivery of content to your website.

Follow the exercise instructions described below:

**Step 1. Create S3 Bucket**
From the AWS Management Console page, select the S3 service.
Use the Create bucket wizard to create a bucket

![CloudFront](./images/cloudfront.png)


**Step 2. Upload Object to Bucket**

- Once the bucket is open to view its contents, click the Upload button to add files/folders.
- Click the Add Files button, and upload the Sample.html (or any file from your local computer) provided at the bottom of the current page.
- Note that the Bucket has not allowed public access, therefore, the Sample.html file cannot be accessed via its object URL, such as https://my-014421265158-bucket.s3.us-east-2.amazonaws.com/Sample.html.

> Note - In the steps above, the object URL will be different in your case.
![CloudFront1](./images/cloudfront1.png)
![CloudFront2](./images/cloudfront2.png)
![CloudFront3](./images/cloudfront3.png)

**Step 3. Create CloudFront Distribution**
- Select the CloudFront service from the Services menu at the top left corner of your AWS console.
- Start the Create Distribution wizard.
- Under the Web delivery method, click the Get Started button, and use the following details to create a distribution:

![CloudFront_conf](./images/cloudfront_conf.png)


> In the configuration table above, the Grant Read Permission on Bucket says that "Yes, update access bucket policy automatically to allows the Origin Access Identity user access to the bucket content." Origin Access Identity user represents the CloudFront service. The policy is a JSON file that defines the access permissions to the bucket object.

- Leave the defaults for the rest of the options. It may take up to 10 minutes for the CloudFront Distribution to get created. Upon successful creation of the CloudFront distribution, the S3 bucket access policy will also get updated automatically, as shown below.

![CloudFront4](./images/cloudfront4.png)


- Once your CloudFront distribution is created, and the status shows as Deployed, copy its Domain Name (such as, dgf7z6g067r6d.cloudfront.net) and append /Sample.html before pasting it in a new browser.
- For the initial few attempts, your https://dgf7z6g067r6d.cloudfront.net/Sample.html may redirect to https://my-014421265158-bucket.s3.us-east-2.amazonaws.com/Sample.html, which is why you may still see an AccessDenied error.

> Note - Remember, as soon as your CloudFront distribution is Deployed, it attaches to S3 and starts caching the S3 private pages. Once the caching is complete, the CloudFront domain name URL will stop redirecting to the S3 object URL. CloudFront may take 10-30 minutes (or more) to cache the S3 page, and you will be able to view the webpage, as shown below.

> Note - In the steps above, the exact domain name and the object URL will be different in your case.

![CloudFront5](./images/cloudfront5.png)

**External Resources**
Good to read - [Restricting access to S3 content by using an Origin Access Identity](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-restricting-access-to-s3.html#private-content-granting-permissions-to-oai) 

**Step 4. Delete Bucket and Distribution**
1. Delete the CloudFront distribution

  - On the Distributions dashboard, click on the radio button next to the Delivery Method for the distribution. Click Disable, and confirm the prompt.


  - Once the distribution is disabled, you can delete it by selecting the radio button next to the Delivery Method and clicking the Delete button.


  - You may also need to delete the Origin Access Identity users. To do so, you can go to the Origin Access Identity service in the CloudFront dashboard.

  
![CloudFront6](./images/cloudfront6.png)

2. Delete de s3 Bucket.



## Security ##




### AWS Web Application Firewall ###

AWS WAF

AWS WAF (or AWS Web Application Firewall) provides a firewall that protects your web applications. WAF can stop common web attacks by reviewing the data being sent to your application and stopping well-known attacks.

Tips
WAF is found under the Security, Identity, & Compliance section on the AWS Management Console.
WAF can protect web sites not hosted in AWS through Cloud Front.
You can configure CloudFront to present a custom error page when requests are blocked.
AWS WAF is available under a composite dashboard, WAF & Shield, that combines the following three services:

1. AWS WAF: It allows you to protect your web applications from common web exploits by monitoring and controlling the web requests coming to an Amazon API Gateway API, an Amazon CloudFront distribution, or an Application Load Balancer.
2. AWS Shield: It provides continuous DDoS attack detection and automatic mitigations. AWS Shield offers two tiers of protection - Standard and Advanced.
3. AWS Firewall Manager: It allows you to configure and manage firewall rules across accounts and applications centrally.
Within AWS WAF service, you can create Web access control lists (web ACLs) to monitor HTTP(S) requests for AWS resources. You can protect the following types of resources:

- CloudFront distributions
- Regional resources (Application Load Balancer, API Gateway, AWS AppSync)
While creating a web ACL, you add rules, such as conditions like originating IP addresses, that determines whether to allow/block each request.


AWS WAF prevets from two web attacks:
- sql injection
- cross-site scripting



### AWS Shield ###


AWS Shield is a managed DDoS (or Distributed Denial of Service) protection service that safeguards web applications running on AWS. AWS Shield offers two tiers of protection - Standard and Advanced.

Standard tier: Standard AWS Shield is a service that you get "out of the box", it is always running (automatically) and is a part of the free standard tier.
Advanced tier: If you want to use some of the more advanced features, you'll have to utilize the paid tier.
> The standard AWS Shield Standard is always-on, using techniques to detect malicious traffic.


If you want to view the threat-event summary for resources in your account, you will have to subscribe to the Shield Advanced. The summary will include statistics, such as total events, largest bit rate, largest packet rate, and the largest request rate.


### IAM ###


1. IAM User
A user is a unique identifier generated by the IAM service and recognized by all AWS services to grant access to AWS resources. A user can be a person, system, or application that requires access to AWS services. You can generate login credentials and access keys for any user in your account. Roles and policies control the scope (permissions) of a user's access to AWS resources in your account.

2. IAM Group
A group collects IAM users with the same level of permissions to access AWS resources. You can attach or detach permissions to a group using access control policies. A group makes it easier to manage IAM users with the same level of permissions.

3. IAM Role
A role is simply a set of policies (permissions) to access AWS services. You can assign a role either to an IAM user or an AWS service such as EC2. Creating and storing roles helps to delegate access with defined permissions without sharing long-term access keys.

Difference between an IAM role and an IAM user
An IAM user has permanent credentials that can be used to interact with AWS services directly. In contrast, an IAM role does not have any credentials; hence it cannot make direct requests to AWS services. IAM roles are assumed by authorized entities, such as IAM users, applications, or other AWS services.

4. IAM Policy
An access control policy is a JSON file that defines the resource to grant access, level of access, and allowed actions. You can attach a policy to multiple users, groups, or roles to assign permissions to AWS resources.


See a sample IAM policy that allows full EC2 access within a specific AWS region:
`
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": "ec2:*",
            "Resource": "*",
            "Effect": "Allow",
            "Condition": {
                "StringEquals": {
                    "ec2:Region": "us-east-2"
                }
            }
        }
    ]
}
`



You can have a look at many more managed policies here: [Example IAM identity-based policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_examples.html) 

**How do I know if my custom policy is having the desired access permissions?**
AWS offers a utility, [IAM policy simulator](https://policysim.aws.amazon.com/) , where you can evaluate, and validate the effects of your access control policies.

**Recommended Read**
1. StackOverflow discussion - [Difference between IAM role and IAM user in AWS](https://stackoverflow.com/questions/46199680/difference-between-iam-role-and-iam-user-in-aws)
2. In addition to IAM policies, AWS offers other types of policies, such as an S3 Bucket Policy, an SNS Topic Policy, a VPC Endpoint Policy, and an SQS Queue Policy. There is a helpful utility, AWS Policy Generator, that can generate either of the policies mentioned above.
3. AWS IAM FAQs - must read.


## Networking and Elasticity ##

### Route 53 ###
Route 53 is a cloud domain name system (DNS) service that has servers distributed around the globe used to translates human-readable names like www.google.com into the numeric IP addresses like 74.125.21.147.

**Features**
scales automatically to manage spikes in DNS queries
allows you to register a domain name (or manage an existing)
routes internet traffic to the resources for your domain
checks the health of your resources
Tips
Route 53 is found under the Networking & Content Delivery section on the AWS Management Console.
Route 53 allows you to route users based on the user’s geographic location.


### EC2 Auto Scaling ###

EC2 Auto Scaling is a service that monitors your EC2 instances and automatically adjusts by adding or removing EC2 instances based on conditions you define in order to maintain application availability and provide peak performance to your users.

**Features**
- Automatically scale in and out based on needs.
- Included automatically with Amazon EC2.
- Automate how your Amazon EC2 instances are managed.
**Tips**
- EC2 Auto Scaling is found on the EC2 Dashboard.
- EC2 Auto Scaling adds instances only when needed, optimizing cost savings.
- EC2 predictive scaling removes the need for manual adjustment of auto scaling parameters over time.


You can know when EC2 Auto Sclaing is launching or terminating an instance Via a messaging service the Simple Notification Service.


### EC2 - Create Auto Scaling group ###



EC2 Auto Scaling is a service that ensures you have the desired number of EC2 instances always up and running to handle the expected load for your application. To set-up an Auto Scaling group, you require the following basic details:

1. Count of instances - The desired count of the EC2 instances you want to have available. If any instance goes down/fails, a new instance automatically spins up.

2. Launch template - The auto scaling group contains a collection of EC2 instances that are treated as a logical group. All EC2 instances within a group share the same configuration. Therefore, You need to specify the configuration details, such as, the ID of the Amazon Machine Image (AMI), the instance type, a key pair, security groups, and the other parameters that you use to launch EC2 instances. You specify the configuration details in a Launch template.

3. Scaling policy - The auto scaling policy that defines how to scale your EC2 instances automatically, based on demand

**A. Start the Auto Scaling Groups service**
Go to the EC2 Dashboard, and select the Auto Scaling Groups service from the left navigation pane. See the snapshot below. For first time users, it may take you to the homepage. Please devote a moment to read through the introduction.


![AutoScale0](./images/AutoScale0.png)

**B. Create an Auto Scaling group**

The **Create Auto Scaling group** is a seven-step process, as shown in the snapshot below. Provide a launch template or configuration in the first step. AWS prefers launch templates over launch configuration files. (Although, both convey similar information.) If you do not have a pre-created launch template, you can create a launch template from the current step.

![AutoScale](./images/AutoScale1.png)


In the remaining steps, you can configure group size, scaling policies, notifications settings, and tags. The group size allows you to mention the minimum, maximum, and desired number of instances in the group, such that min <= desired <= max. For scaling policies, you can create and add either a step/simple/target scaling policy.

**Launch template**
As mentioned above, a launch template specifies the configuration details, such as, the ID of the Amazon Machine Image (AMI), the instance type, a key pair, security groups, and the other parameters that you use to launch EC2 instances. See a quick video below to see the information available in a launch template.



### EC2: Auto Scaling Group ###


Let's have a walkthrough of an Auto Scaling Group which has already been created.

**1. Select an Auto Scaling Group**
Go to the EC2 Dashboard, and select the Auto Scaling Groups service from the left navigation pane. Select an Auto Scaling Group which has already been created.

![ASG0](./images/ASG0.png)


**2. View Details of the Selected Auto Scaling Group**
Once you select an Auto Scaling Group, you can view further details, as shown in the snapshots below.

![ASG1](./images/ASG1.png)


**3. Launch template**
A Launch Template specifies instance configuration information, such as, the ID of the Amazon Machine Image (AMI), the instance type, a key pair, security groups, and the other parameters that will be used to launch EC2 instances.

View the Launch template used in the current Auto Scaling group. In the snapshot below, we have the following configuration:

- Amazon Linux 2 AMI
- t2.nano instance type
- An existing key pair to log in to the EC2 instances. We have kept the rest of the other things as default.

![ASG2](./images/ASG2.png)

**4. Activity**
On the activity tab, the Status column shows the current status of your instances. In the snapshot below, notice that we have a list showing that one instance was created initially, and later it was terminated. Consequently, the auto scaling group has automatically spun up a new instance.

While your instance is launching, the status column shows In progress. The status changes to successful after the instances are launched.

You can also use the "Refresh" button to see the current status of your instances.

![ASG3](./images/ASG3.png)

**5. Auto Scaling**
Scaling policies allow you to dynamically scale your Amazon EC2 capacity automatically, based on demand. You can create and add either a step /simple/target scaling policy.

![ASG4](./images/ASG4.png)

**6. Instances Management**
View the list of instances running as part of the current group. In the snapshot below, you can see that your autoscaling group has launched your EC2 instance and that it is InService. Similarly, you can view other details, such as AZs, and the health status of each instance.
![ASG5](./images/ASG5.png)

**7. Instance refresh**
An instance refresh allows you to trigger a rolling replacement of all previously launched instances in the Auto Scaling group with a new group of instances.
![ASG6](./images/ASG6.png)



### Elastic Load Balancer ###


- Balance load between 2 or more servers. 
- Stands in front of a web server.
- Provide Redundancy and performance.
  - **Redundancy**: If you lose a server, the load balancer will send request to other working server.
  - **Performance** If your servers have issues or bottleneck, the load balancer will add more server to the pool of available servers. 

**Tips**

- Elastic Load Balancing can be found on the EC2 Dashbaoard.
- Elastic Load Balancing works with EC2 Instances, containers, IP addresses, and Lambda functions.
- You can configure Amazon EC2 instances to only accept traffic from a load balancer.


**Create a Load Balancer**


**A. Prerequisite**
Go to the EC2 dashboard. In order to use elastic load balancing, you will need to make sure that you've launched the EC2 instances that you plan to register with your load balancer.

> You must have more than one EC2 instance in the running state. In our example snapshot below, we have two instances, in two different availability zones (AZs).

![ELB0](./images/ELB0.png)

**B. Start the Load Balancer service**
On the EC2 dashboard, select the Load Balancers service from the navigation pane on left. Here, you can view the list and details of existing load balancers.
![ELB1](./images/ELB1.png)

Launch the Create Load Balancer wizard. AWS offers three types of load balancers, as shown below.
![ELB2](./images/ELB2.png)

1. Application Load Balancer (ALB)
A simple use case: Assume you are running a microservices-architecture based application. An Application Load Balancer allows you to host the different API endpoints of your application on different servers. The load balancer then redirects the incoming HTTP/HTTP traffic to the suitable server based on the rules you specify in the configuration.

If you choose this option, you will be taken to a six-step process:

- Configure Load Balancer
- Configure Security Settings
- Configure Security Groups
- Configure Routing
- Register Targets
- Review
 
**2. Network Load Balancer (NLB)**
A Network Load Balancer helps to balance the load on each individual server. Having an NLB becomes essential when your application requires handling millions of requests per second securely while maintaining ultra-low latencies.

This option has a five-step process:

- Configure Load Balancer
- Configure Security Settings
- Configure Routing
- Register Targets
- Review

See an example NLB below:
![ELB3](./images/ELB3.png)

**3. Classic Load Balancer (CLB)**
It is a previous generation option. You can choose a Classic Load Balancer when you have an existing application running in the EC2-Classic network. You will have to follow a seven-step process to create a CLB:

- Define Load Balancer
- Assign Security Groups
- Configure Security Settings
- Configure Health Check
- Add EC2 Instances
- Add Tags
- Review

See an example CLB below:
![ELB4](./images/ELB4.png)




The CLB in the snapshot above is balancing the load between two of our EC2 instances: Server_1 and Server_2. If you click on the Instances tab, you're able to see the two instances that this load balancer is managing. You have the option to add or remove instances simply by clicking on Edit instances.

### EC2: Lab NLB ###

Prerequisites:
- An AWS account
- A default VPC. It is a VPC in a default region and has a public subnet in each Availability Zone. Refer to the create a default VPC for more details. Just to ensure you have the right set of VPC, subnet, route table, and internet gateway available, refer to the snapshots below.


![NLB0](./images/NLB0.png)
![NLB1](./images/NLB1.png)
![NLB2](./images/NLB2.png)
![NLB3](./images/NLB3.png)
Prerequisite 2: Subnets in each AZ in the default VPC. Also, notice that a common route table is attached to all subnets.
![NLB4](./images/NLB4.png)

Prerequisite 3: A route table with a rule for internet facing communication. See that it requires an internet gateway


![NLB5](./images/NLB5.png)
Prerequisite 4: The Internet gateway is a managed service. See an internet gateway attached to the default vpc.


Step 1. Create the first EC2 instance
The steps below show how to create the first EC2 instance in a public subnet in any one Availability Zone, and install the Apache webserver on it. Use the following configuration, and leave the remaining values as the defaults.

Navigate to the EC2 Dashboard page, and click on the Launch Instance wizard to launch an instance. Choose the AMI and instance type as:
| Step                          | Value                                     |
| ---                           | -------------                             |
| 1. Amazon Machine Image (AMI) | Amazon Linux 2 AMI (HVM), SSD Volume Type |
| 2. Instance Type              | t2.micro                                  |
- **At the next step, Configure Instance Details, use the following values:**

| Field                 | Value                                                           |
| -----                 | ----                                                            |
| Number of Instances   | 1                                                               |
| Network               | Select the default VPC that has public subnets in different AZs |
| Subnet                | Choose anyone, say us-east-2a                                   |
| Auto-assign Public IP | Enable                                                          |

- Let's add advanced details.
![NLB6](./images/NLB6.png)
Under the Advanced Details → User data section, add the following configuration script to run automatically during launch.
```bash
#!/bin/bash
sudo yum update -y
sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2
sudo yum install -y httpd mariadb-server
sudo systemctl start httpd
sudo systemctl enable httpd
sudo chkconfig httpd on
# Set file permissions for the Apache web server
sudo groupadd www
sudo usermod -a -G www ec2-user
sudo chgrp -R www /var/www
sudo chmod 2775 /var/www
find /var/www -type d -exec sudo chmod 2775 {} +
find /var/www -type f -exec sudo chmod 0664 {} +
# Create a new PHP file at  /var/www/html/ path
echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php
```

The script above will install, configure, and launch the Apache webserver on the EC2 instance. You can learn more about the individual steps at Create an EC2 instance and install a web server.
![NLB7](./images/NLB7.png)


- Keep the storage as default, and use a tag as Name: Server-A
- At the Configure Security Group step, you can create a new one, and ensure to have a firewall rule to allow incoming HTTP traffic on port 80.

| Type | Protocol | Port | Source    |
| ---  | --       | ---  | ---       |
| HTTP | TCP      | 80   | 0.0.0.0/0 |
| SSH  | TCP      | 22   | 0.0.0.0/0 |

- **The step above is crucial for the current experiment.**

![NLB8](./images/NLB8.png)


- Generate and download a new key pair, at the last stage of the Launch Instance wizard.
Important: This key-pair will allow you to log into your instance, using SSH, from your local machine. Save the key-pair carefully, because the same private key cannot be re-generated.



**Step 2. Create the second EC2 instance, in a separate Availability Zone**

Launch the second EC2 instance using the same steps above, except for the following changes at the Configure Instance Details step:

- Select another public subnet in a different AZ, say us-east-2b
- Replace the last line of the user data (shell script) with

```bash
echo "<? echo "<h1>Welcome to server 2</h1>" ?>" > /var/www/html/phpinfo.php
```

- Change the tag to `Name: Server-B`

**Step 3. Verify the Apache webserver installation**

- Confirm that the newly created EC2 instances are in the running state.


![NLB9](./images/NLB9.png)
Two instances running in different AZs. Server-A is running in us-east-2a, while Server-B is running in us-east-2b.


- Verify that the Apache server is running successfully on both the EC2 instances. Simply copy, and paste the public IPv4 address of each instance in a new browser window. If the Apache is configured successfully, you will see the Apache welcome page.
> Note: We have opened the HTTP traffic on the default port, therefore the public IPv4 address should be prepended with http://, instead of https://.

- Configuring the secure HTTPS on EC2 will add overhead to the current experiment, and you may deviate from the intent of learning an NLB.
> Need help?: Refer to the How do I troubleshoot an unresponsive website hosted on my EC2 instance or clean restart the exercise by deleting the VPC, and EC2 resources again.
![NLB10](./images/NLB10.png)

View the content of the PHP page that you configured using the shell script.

![NLB11](./images/NLB11.png)


**Step 4. Create an NLB**
- Select the Load Balancers service on the left-hand side menu of the EC2 dashboard, and click on the Create Load Balancer button.
![NLB12](./images/NLB12.png)

- You will be prompt to choose the type of load balancer: Application, Network, or Classical load balancer. Choose to create a Network Balancer.
- At the first step, Configure Load Balancer, use the following basic configuration details


| Section             | Field           | Value              |
|---------------------|-----------------|--------------------|
| Basic Configuration | Name            | udacity-nlb        |
| Scheme              | internet-facing |                    |
| Availability Zones  | VPC             | Choose default-vpc |
||Availability Zones|	Check the two where you've launched the EC2 instances, such as us-east-2a and us-east-2b|

See the snapshot below:

![NLB13](./images/NLB13.png)

- Skip the Configure Security Settings step, by clicking the Next button.
- At the Configure Routing step, use the following configuration details in the Target group section:

| Field        | Value            |
| -            | -                |
| Target group | New target group |
| Name         | UdacityNLBTarget |
| Target type  | Instance         |
| Protocol     | TCP              |
| Port         | 80               |

- At the Register Targets step, add the two EC2 instances created previously to the target group.


![NLB14](./images/NLB14.png)


Add instances to the registered target group. Do not forget to click on the Add to registered button after selecting the instances from the list.

- Leave the remaining things as default, and finish creating the NLB.

- **Step 5. Test the NLB**
- You will be taken back to the Load Balancers dashboard. Copy the DNS name of the newly created NLB, and append the /phpinfo.php at the end of it. A sample DNS name appended with the file name looks like this:
`http://udacity-nlb-f00b2cb9e62f5c2a.elb.us-east-2.amazonaws.com/phpinfo.php`

- Paste the copied DNS name to a new browser window and refresh the browser a few times, each after a few seconds. You will notice that sometimes the request is redirected to Server-A and other times, it is routed to Server-B.

![NLB15](./images/NLB15.png)




### EC2 Auto Scaling ###

In this hands-on exercise, you will use Auto Scaling to automatically launch Amazon EC2 instances in response to the conditions you specify. You will also see auto-scaling in action as it automatically provisions replacement instance(s).

> Definition: An Autoscaling group contains a collection of EC2 instances that share similar characteristics and are treated as a logical group.

All EC2 instances that are provisioned as a part of auto-scaling have the same configuration because they are instantiated from a Launch template. Let's get started.

**Preparatory Steps**
1. Sign in to the AWS Management Console.
2. Navigate to the EC2 dashboard. In this exercise, we will use the following two services available in the EC2 dashboard:
   - Instances → Launch templates
   - Auto Scaling → Auto Scaling Groups
 
**Stage 1. Create a Launch template**
> Definition: A Launch template specifies instance configuration information, such as, AMI ID, the instance type, a key pair, security groups, and the other parameters that you use to launch EC2 instances.

1. Go to the Launch templates service, and create a new template by specifying the following parameters:
  - Template name, and description of your choice.
  - Template contents:
    - AMI ID: Amazon Linux 2 AMI (HVM), SSD volume type
    - Instance type: t2.micro
    - Key-pair for logging in to the EC2 instances: Your choice of key-pair
    - Network settings: Choose a Virtual Private Cloud (VPC), and a subnet in which the network interface is located. Choose a security group accordingly, because this step will ensure that a public IP address is assigned automatically to every instance.
    - Storage (volumes), tags, and network interfaces: Default
    
**Stage 2. Create an Autoscaling group**

1. Go to the Auto Scaling Groups service, and create a new Autoscaling group. Creating an Autoscaling group is a multi-step process, in which you specify the configuration settings, group size, scaling policies (step/simple/target scaling policy), notifications, and tags. For this exercise, you have to specify the following minimal set of configurations:
  - Choose a Launch template that you have created in the previous step.
  - Provide the VPC, and subnets in which you want to create your EC2 instances.
  - Specify the Group size with the desired, minimum, and maximum capacity, i.e., count of EC2 instances at any given moment. You can choose the default value, 1, for each capacity.
  - Use the default values in the remaining steps of this process.
  
**Stage 3. Verify your Autoscaling group**
1. On the Auto Scaling Group dashboard, select the Autoscaling group that you have created in the step above.

2. Verify the details that were provided while creating the Autoscaling group.

  - Verify that the Autoscaling group has launched the desired number of EC2 instance(s). The status of your instance(s) should be Successful, which means the instances are launched.

  - Verify that the instances have the desired lifecycle and health. Also, note the Instance ID for the next step.

**Stage 4. Test Autoscaling group**
In this step, you will terminate only those instance(s) that were launched as a part of the Autoscaling group. And, then we will verify if the Autoscaling group automatically launches new instances to maintain the desired number of running instances.

> Note - In addition to the instances that are launched as a part of the Autoscaling group, it is possible that you have additional instances already created in your EC2 dashboard.

1. Go to the EC2 Instances dashboard, and select the instance(s) that you want to terminate.
2. Terminate the selected instance(s).
3. Go back to the Auto Scaling Group service and select the Autoscaling group that you have created in the step above.
4. While viewing the details of the Autoscaling group, review the history for the EC2 instance(s). You will see that the previous EC2 instance has been terminated, and a new one(s) are being instantiated.

**Stage 5. Delete Autoscaling group resources**

In order to avoid being billed unnecessarily, it is important to delete the resources provisioned during this exercise.

- Come back on the Auto Scaling Group dashboard, and select the checkbox against the auto-scaling group you want to delete.
- At the top of the screen, click the Delete option.


## Messaging and Container ##

### Simple Queue Service (SQS) ###

Amazon Simple Queue Service (SQS) is a fully managed message queuing service that allows you to integrate queuing functionality in your application. SQS offers two types of message queues: standard and FIFO.

**Features**
- send messages
- store messages
- receive messages

**Tips**
- The Simple Queue Service (SQS) is found under the Application Integration on the AWS Management Console.
- FIFO queues support up to 300 messages per second.
- FIFO queues guarantee the ordering of messages.
- Standard queues offer best-effort ordering but no guarantees.
- Standard queues deliver a message at least once, but occasionally more than one copy of a message is delivered.


### SNS Lab ###


In this hands-on exercise, you will learn how to send alerts via SNS by creating a topic, subscribing to a topic, and publishing an alert message to a topic.

1. Prerequisites: AWS Account
2. By the end of this lab, you will be able to:
  - Create a topic
  - Subscribe to a topic
  - Publish a message to a topic
Follow the exercise instructions described below:

**Step 1. Create a Topic**

- From the AWS Management Console page, select the SNS service.
- On the left-hand navigation pane, click on the Topics service, and start the Create topic wizard.
- In the Details section, enter a topic name of your choice
- In the Access policy – optional section, use the following configuration to create the topic:

| Configuration                                | Value    |
| -                                            | -        |
| Policy method                                | Basic    |
| Define who can publish messages to the topic | Everyone |
| Define who can subscribe to this topic       | Everyone |
- Finish the Create topic. The topic details will display, or you can select the newly created topic from the Topics dashboard to create a subscription next.

**Step 2. Subscribe to a Topic**
- While you are viewing the details of the newly created topic, start the Create subscription wizard, and use the following details:


| Field    | Value                                                  |
| -        | -                                                      |
| Protocol | Email                                                  |
| Endpoint | Enter your email that should receive the notifications |

- The subscription page will display, and the status will be Pending confirmation. You will receive an email from Amazon SNS to confirm the subscription. Confirm the subscription.
- In your web browser, a subscription confirmation screen appears.




**Step 3. Publish Message to a Topic**
- Go back to the Topics service.
- Select the topic you created earlier and Publish a message with the following details:

| Section            | Field                                | Value                                                  |
| -                  | -                                    | -                                                      |
| Message details    | Subject                              | Wishes                                                 |
| Message body       | Message body to send to the endpoint | Congratulations on your Udacity Nanodegree Graduation! |
| Message attributes | Type, Name, Value                    | String, Occasion, Graduation                           |

- In your email client, you will receive an email from AWS Notifications (no-reply@sns.amazonaws.com)

### Elastic Containre Services (ECS) ###


**What is Elastic Container Service (ECS)?**
ECS is an orchestration service used for automating deployment, scaling, and managing of your containerized applications. ECS works well with Docker containers by:

- launching and stopping Docker containers
- scaling your applications
- querying the state of your applications

**Tips**
- ECS falls under the Compute section on the AWS Management Console.
- You can schedule long-running applications, services, and batch processeses using ECS.
- Docker is the only container-runtime platform supported by Amazon ECS. Other container-runtime tools available in the insdustry are Rocket, LXD, OpenVZ, any a few more.


**ECS** is usefull for:
- Deployment automation
- Automatic Scalling
- Application Management



**How does Amazon ECS helps?**
Assume you have a multi-container application that you want to run on the cloud. You may also require to scale the containers automatically based on the incoming traffic in such a case.

Amazon ECS deploys, manages, and scales containers based on your resource needs and supports other AWS services like Elastic Load Balancing, EC2 security groups, EBS volumes, and IAM roles.

**Key terms related to Amazon ECS**
1. Task definition
A task definition describes the application requirements concerning containers, such as the max amount of total CPU and memory used for the task (not for the individual container) and container definitions.

ECS offers to create a task definition using either the AWS Fargate or AWS EC2. AWS Fargate is priced based on the task size, whereas the EC2 service is priced based on computing resource usage.


You can create a task definition using either the AWS Fargate or AWS EC2

Either way, you can add a container definition, as shown in the snapshot below.


![ECS](./images/ECS.png)


2. ECS cluster
A cluster is a set of containers running task requests within an AWS region. A default cluster gets created when you create and run your first task definition.
3. Container agent
It is a utility that connects container instances to one of your clusters. Each container instance runs a container agent.
4. Container instance
A container instance is an EC2 instance that is registered into any of your ECS clusters.

### ECS - Create a Cluster ###



In this hands-on exercise, you will learn how to create a Cluster in Amazon ECS.

Follow these steps to create a Cluster in ECS.

1. Navigate to the ECS dashboard, and select the Clusters service from the left-hand side menu pane.
2. On the Clusters page, choose the Create cluster button.

![ECS1](./imges/ECS1.png)

3. At the Select cluster template step, choose the Networking only compatibility.
![ECS2](./imges/ECS2.png)


Choosing the Networking only template, that allows creating a cluster and optionally create a VPC, and subnets.

4. At the Configure Cluster step, enter the name for your cluster. Choose a unique name.
5. In the Networking section, create a new VPC for your cluster. You can keep the default settings for the subnet division.
![ECS3](./imges/ECS3.png)

6. Enable the CloudWatch container insights. And finally, click the Create button.




## AWS Management ##


**Logging In The Cloud**
Logging provides visibility into your cloud resources and applications. For applications that run in the cloud, you will need access to logging and auditing services to help you proactively monitor your resources and applications.

Logging allows you to answer important questions like:

How is this server performing?
What is the current load on the server?
What is the root cause of an application error that a user is seeing?
What is the path that leads to this error?

### Cloud Trail ###

Cloud Trail allows you to audit (or review) everything that occurs in your AWS account. Cloud Trail does this by recording all the AWS API calls occurring in your account and delivering a log file to you.
Features
CloudTrail provides event history of your AWS account activity, including:

- who has logged in
- services that were accessed
- actions performed
- parameters for the actions
- responses returned
This includes actions taken through the AWS Management Console, AWS SDKs, command line tools, and other AWS services.

**Tips**
- Cloud Trail is found under the Management & Governance section on the AWS Management Console.
- CloudTrail shows results for the last 90 days.
- You can create up to five trails in an AWS region.


You can also set alets and alarms if certain activities occur.


### CloudTrail - Create a Trail ###


> AWS CloudTrail is a service that captures every event occurred in your account, in the form of logs, for review and analysis. These logs can be stored in Amazon S3 buckets or delivered to Amazon CloudWatch logs, which helps you to set alarms and take appropriate actions.

Let's see how to create a trail, and view the details of an existing trail.

**A. CloudTrail Dashboard**
Navigate to the CloudTrail dashboard, and launch the wizard to create a trail.


**B. Create a Trail**
AWS provides a quick trail create process, where you just have to specify the display name for your trail, and an S3 bucket to store logs.

1. **Quick process**
The Quick trail create wizard will automatically create an S3 bucket and folder on your behalf to store the logs. The folder in the newly created S3 bucket is `aws-cloud trail-logs-014421265158-1acfb819`, and the folder is `AWSLogs/014421265158/CloudTrail/`. It will create further sub-folders based on your region name, year, month, and date. An example (auto-generated) file created at the above mention path in the S3 bucket is:


`014421265158_CloudTrail_us-east-1_20201126T1225Z_AumNC3WbMzJTBiSR.json.gz`

![CloudTrail0](./images/CT0.png)

2. **Regular process**
If you wish to use an existing S3 bucket, you will have to navigate to the detailed Create trail process. You can launch one from the CloudTrail dashboard. The regular Create trail is a three-step process:

1. Step 1 - General details - Provide the trail name, choose the new/existing S3 bucket, and enable/disable the encryption.

If the encryption is enabled, CloudTrail will encrypt log files by using the AWS Key Management Service (SSE-KMS). In addition, you can choose to be notified each time a log is delivered to your bucket. There is another feature, log digest, to verify that your log files did not change after CloudTrail delivered them.


2. Step 2 - Events and Management details - Choose the types of events you want to log. There are three categories of events - Management events, Data events (operations performed within a resource), and Insights events (unusual activity, errors, or user behavior).

![CloudTrail1](./images/CT1.png)
![CloudTrail2](./images/CT2.png)
**C. Dashboard**
The CloudTrail dashboard displays an overview of all your trails, insights, and event history.

> Consider a Trail as a log of all the events/actions that occurred in your AWS account. Of course, events have to be processed to convert them into a particular log-format.

![CloudTrail3](./images/CT3.png)

- In the snapshot above, notice the separate table for Trails, Insights, and Event history. The Event history section shows all the recent events. It shows every action that occurred in your AWS account. Click on View full Event history to see additional details and more events that have occurred.
- Remember, that the first trail does not attract billing charges. However, you incur charges for the S3 bucket that will store your logs. You can create additional trails on a charge-basis.
> Recently AWS has launched a new feature - Event comparison to compare up to five events from the Event history. You can download the full or filtered event history.


### Cloud Watch ###


Cloud Watch is a service that monitors resources and applications that run on AWS by collecting data in the form of logs, metrics, and events.

Features
There are several useful features:

- Collect and track metrics
- Collect and monitor log files
- Set alarms and create triggers to run your AWS resources
- React to changes in your AWS resources

**Tips**
- CloudWatch is found under the Management & Governance section on the AWS Management Console.
- Metrics are provided automatically for a number of AWS products and services.


Uses of Cloud Watch:
1. Trigger a Lambda
2. Capture log files from services
3. Track metrics

### Cloud Watch Labs ###


In this hands-on exercise, you will create a Cloud Watch event to notify via an SNS topic when an EC2 instance is created.

1. Prerequisites:

  - AWS account
  - SNS Topic created in the previous lab
2. By the end of this lab, you will be able to:

  - Create Cloud Watch event to react to the creation of an Amazon EC2 instance
  - Send SNS notification via Cloud Watch when an event occurs
  
Follow the exercise instructions described below:

**Steps:**
**1. Create CloudWatch Rule**
- Navigate to the CloudWatch service.
- On the left-hand menu, under `Events`, select `Rules.`
- Click on the `Create rule` button.
- For `Service Name`, select `EC2`.
- For the `Event Type`, select `EC2 Instance State-change Notification.`
- Select the `Specific state(s)` radio button. Select `running` from the drop-down box.
> Note: This configures the rule to trigger whenever an Amazon EC2 instance changes to the running state, which happens when an instance is launched or started.

- On the right-hand side of the screen, in the `Target` section, add a target by clicking on `Add target.`
- In the drop-down, change `Lambda function` to `SNS topic.`
- For the `Topic`, select the topic you created in the SNS hands-on exercise.
> Important: If the Topic doesn’t appear, the `Access policy – optional` section doesn’t have the correct permissions to allow other services to access the Topic.

- Scroll down and click the `Configure details`.
- Enter a name in the `Name` field. Ensure the state is `Enabled`. Click `Create rule`.

**2. Test CloudWatch Rule**
- Navigate to the EC2 console page, by clicking on `Services` in the upper left-hand menu. Type EC2 in the text box and click on EC2 found in the search results.
- On the EC2 Dashboard page, click on `Instances` in the left-hand navigation.
- Click `Launch Instance`.
- Select the `Amazon Linux 2 AMI (HVM), SSD Volume Type` Amazon Machine Image (AMI). Important: You are free to choose a different AMI, but to avoid excessive charges, pick one that says, Free Tier Eligible.
- For the `Instance Type`, select the free-tier instance type of `t2.micro`.
- Click `Review and Launch`.
- Click `Launch`.
- Generate and download a new key pair and then launch the instance.
- Click `Launch Instances`.
- Click on `View Instances`.
- Once the Instance state changes to `Running`, check your email client for an email alert from the SNS Topic.

**3. Cleanup & Disable EC2 Instance and Cloud Watch Rule**
- To avoid recurring charges for leaving an instance running, let’s disable the EC2 instance.
- From the EC2 Dashboard, select the instance just created, click `Actions`, then `Instance State`, and then select `Terminate`.
- To avoid recurring charges for leaving the Cloud Watch rule running, let’s disable it.
- From the CloudWatch Dashboard, select `Rules` from under the `Events` section.
- Select the Rule you just created, by clicking the radio button next to the Rule.
- Click on the `Actions` button, and select `Delete`.



### Infrastructure as Code ###


Infrastructure as Code allows you to describe and provision all the infrastructure resources in your cloud environment. You can stand up servers, databases, runtime parameters, resources, etc. based on **scripts that you write**. Infrastructure as Code is a time-saving feature because it allows you to provision (or stand up) resources in a reproducible way.


### Lab: Cloud Formation ###

In this hands-on exercise, you will create an S3 bucket with AWS CloudFormation.

1. Prerequisites: AWS account

2. By the end of this lab, you will be able to:

- Create a CloudFormation stack using the CloudFormation Designer
- Launch S3 bucket using Infrastructure as Code
- Save and deploy a CloudFormation stack
- View resources created through CloudFormation
Follow the exercise instructions described below:

**Steps:**
**1. Create CloudFormation Stack**
- On the AWS Management Console page, type cloud formation in the Find Services box and then select CloudFormation.
> Important: The redesigned AWS CloudFormation console is available now. This tutorial covers the new designer. To access the new designer, click on the Try it out now and provide us feedback. message that displays in a message similar to what’s shown below.

- If the left-hand menu options do not appear, expand the options by clicking on  in the top left-hand corner.
- Select Designer from the left-hand menu.
- Locate S3 in the Resource Type section and expand it.
- Select Bucket and drag it to the designer window on the right-hand side.
- Copy the JSON below and replace entirely the JSON found in the Properties tab.

```json
{
"AWSTemplateFormatVersion": "2010-09-09",
"Description": "Basic S3 Bucket CloudFormation template",
"Resources": {
"S3BucketCreatedByCloudFormation": {
 "Type": "AWS::S3::Bucket",
 "DeletionPolicy": "Delete",
 "Properties": {
   "AccessControl": "PublicRead"
 }
}
},
"Outputs": {
"BucketName": {
 "Value": {
   "Ref": "S3BucketCreatedByCloudFormation"
 },
 "Description": "Name of the newly created Amazon S3 Bucket"
}
}
}
```

Hit the Refresh button in the upper right-hand corner so that the Designer is not out of date.

**2. Save CloudFormation Stack**
- In the CloudFormation Designer Toolbar, click the Document icon , and click Save.
- Click Local File and click Save. The JSON file will download.
- In the AWS CloudFormation Designer toolbar, click to validate your template. You will see a message that states, Template is valid.

![CF0](./images/CF0.png)


**3. Deploy CloudFormation Stack**
- In the CloudFormation Designer Toolbar, click to deploy the stack. The Create stack screen appears.
- Accept the defaults and click Next.
- Enter a Stack name. Leave Parameters empty. Click Next.
- Leave the defaults and click Next.
- Review the stack details and click Create Stack. The stack status will be CREATE_IN_PROGRESS. To the current status of the stack, select the Refresh button in the upper right-hand corner. Once the stack reaches the CREATE_COMPLETE status, the stack has been deployed.

**4. View S3 Bucket created by CloudFormation Stack**

- From the Services menu option at the top, type in S3 and select S3.
- To quickly find the bucket created by the CloudFormation Stack, click on Date Created in the column heading to sort by the most recent buckets created.
- The newly created bucket appears at the top, cfs3stack-s3bucketcreatedbycloudformation-1at0fv1v9ndc1.

**5. Delete CloudFormation Stack**
- To avoid on-going charges, delete the stack by navigating to the stack, and click the Delete button in the upper right-hand corner.
Note: When the stack is deleted, all resources created by the stack template will also be deleted.



### AWS Command Line Interface (CLI) ###



AWS CLI enables you to run commands to provision, configure, list, delete resources in the AWS cloud. Before you run any of the aws commands, you need to follow three steps:

1. Install AWS CLI
2. Create an IAM user with Administrator permissions
3. Configure the AWS CLI
**Step 1. Install AWS CLI v2**
Refer to the official [AWS instructions to install/update AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html) (version 2) based on your underlying OS. You can verify the installation using the following command in your terminal (macOS)/cmd (Windows).

```
# Display the folder that contains the symlink to the aws cli tool
which aws
# See the current version
aws --version
```

See the sample output below. Note that the exact version of AWS CLI and Python may vary in your system.

**Step 2. Create an IAM user**
In this step, you will create an IAM user with Administrator permissions who is allowed to perform any action in your AWS account, only through CLI. After creating such an IAM user, we will use its Access key (long-term credentials) to configure the AWS CLI locally.

Let’s create an AWS IAM user, and copy its Access key.

> AWS Identity and Access Management (IAM) service allows you to authorize users / applications (such as AWS CLI) to access AWS resources.

The Access key is a combination of an **Access Key ID** and a **Secret Access Key**. Let's see the steps to create an IAM user, and generate its Access key.

1. Navigate to the IAM Dashboard, and create an IAM user.
2. Set the user details, such as the name, and access type as Programmatic access only.
3. Set the permissions to the new user by attaching the AWS Managed AdministratorAccess policy from the list of existing policies.
4. Provide tags [optional], review the details of the new user, and finally create the new user.
5. After a user is created successfully, download the access key file (.csv) containing the Access Key ID and a Secret Access Key. You can even copy the keys and stay on the same page. Don’t skip this step as this will be your only opportunity to download the secret access key file.


**Step 3. Configure the AWS CLI**
You will need to configure the following four items on your local machine before you can interact with any of the AWS services:

1. Access key - It is a combination of an Access Key ID and a Secret Access Key. Together, they are referred to as Access key. You can generate an Access key from the AWS IAM service, and specify the level of permissions (authorization) with the help of IAM Roles.
2. Default AWS Region - It specifies the AWS Region where you want to send your requests by default.
3. Default output format - It specifies how the results are formatted. It can either be a json, yaml, text, or a table.
4. Profile - A collection of settings is called a profile. The default profile name is default, however, you can create a new profile using the aws configure --profile new_name command. A sample command is given below.

If you have closed the web console that showed the access key, you can open the downloaded access key file (.csv) to copy the keys later. It should be something similar to:

```
AWSAccessKeyId=WANI9WATIG63GKCXA89VC74A
AWSSecretKey=kMT2Jn5NPkq1GxtoUqwUbgHtPbsf1ODm/Pbsf1OD
```


- Navigate to the home directory and check the current configuration:

```
# Navigate to the home directory
cd
# View the current configuration
aws configure list
```

- Set the default profile credentials
`aws configure --profile default`

The command above will store the access key in a default file `~/.aws/credentials` and store the profile in the `~/.aws/config` file. Upon prompt, paste the copied access key (access key id and secret access key). Enter the default region as `us-east-1` and output format as `json`.

Let the system know that your sensitive information is residing in the .aws folder

```
export AWS_CONFIG_FILE=~/.aws/config
export AWS_SHARED_CREDENTIALS_FILE=~/.aws/credentials
```


**Step 4. Run your first AWS CLI command**

Check the successful configuration of the AWS CLI, by running an AWS command:

`aws iam list-users`

The output will display the details of the recently created user:
```json
{
"Users": [
    {
        "Path": "/",
        "UserName": "Admin",
        "UserId": "AIDAZMXYZ3LY2BNC5ZM5E",
        "Arn": "arn:aws:iam::388752792305:user/Admin",
        "CreateDate": "2021-01-28T13:44:15+00:00"
    }
]
}
```

**Troubleshoot**
If you are facing issues while following the commands above, refer to the detailed instructions here -

1. [Configuration basics](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html)
2. [Configuration and credential file settings](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html)
3. [Environment variables to configure the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-envvars.html)

**Updating the specific variable in the configuration**
In the future, you can set a single value, by using the command, such as:

```
# Syntax
# aws configure set <varname> <value> [--profile profile-name]
 aws configure set default.region us-east-2
```
It will update only the region variable in the existing default profile.



### Interacting with s3 via cli ###

Hacer todos los pasos para configurar cli.

**Interact with S3 service**

1. Create a public bucket with name `my-033212455158-bucket` in the us-east-1 region, using the newly created `UdacityLab` profile.

`aws s3api  create-bucket --bucket my-033212455158-bucket --acl public-read-write --region us-east-1 --profile UdacityLab`

In the command above,

- --bucket option specifies the bucket name of your choice. It must be unique across all AWS accounts.
- --profile option specifies the profile whose credentials will be verified for authorization before accessing the S3 service. This option is OPTIONAL. If skipped, the aws CLI will use the default profile stored in your system.
- --acl option specifies the accessibility level
- --region specifies the AWS region where you want to create this bucket

Reference - [aws s3api create-bucket command](https://docs.aws.amazon.com/cli/latest/reference/s3api/create-bucket.html)

2. Upload a file to your bucket. The command below uploads a file names Sample.html, however, you can choose any file from your local system.

`aws s3api put-object --bucket my-033212455158-bucket --key Sample.html --body Sample.html --profile UdacityLab`

In the command above,

- --key option specifies the name you want to assign to your object in the bucket
- --body option specifies the file name (complete path) to upload from your local system

Reference [aws s3api put-object](https://docs.aws.amazon.com/cli/latest/reference/s3api/put-object.html)

**Verify the S3 bucket by going to the AWS web console.**

4. Delete the bucket and its content. A bucket can only be deleted if it is empty. Therefore, first delete the Sample.html, and then delete the bucket, as follows:

`aws s3api delete-object --bucket my-033212455158-bucket --key Sample.html`
`aws s3api delete-bucket --bucket my-033212455158-bucket --profile UdacityLab`

Reference - [aws s3api commands](https://docs.aws.amazon.com/cli/latest/reference/s3api/index.html#available-commands)
5. Navigate back to the S3 dashboard (AWS web console), and verify if the bucket has been deleted successfully.



**Step 4. [Optional] Delete the newly created UdacityLab IAM user**
Remember, you created the `UdacityLab` IAM user using the AWS web console. However, you can delete the newly created `UdacityLab` IAM user from your CLI tool as well.

> Note - We are assuming that your AWS root user access key is set in the `default` profile using the command `aws configure --profile default`. Use the `cat ~/.aws/credentials` command to list all the credentials set locally.

1. View the list of all users (other than the root user) in your AWS account.
`aws iam list-users`
2. A user can only be deleted only after deleting the attached user policies, and access key. The commands below are executed using the `default` profile, therefore we have not used the `--profile` option.

```
# List the policies attached to the UdacityLab user
aws iam list-attached-user-policies --user-name UdacityLab
# A policy can be detached using its ARN, a unique identifier
aws iam detach-user-policy --user-name UdacityLab --policy-arn arn:aws:iam::aws:policy/AdministratorAccess
# List the access key for UdacityLab user
aws iam list-access-keys --user-name UdacityLab
# An access key can be deleted using its access key id
aws iam delete-access-key  --user-name UdacityLab --access-key-id AKIAQGW4TBMDIZQP564S
# Delete the user
aws iam delete-user --user-name UdacityLab
```

Reference - [aws iam commands](https://docs.aws.amazon.com/cli/latest/reference/iam/index.html#available-commands)

Navigate back to the IAM console, and access the IAM Users service to verify if the user has been successfully deleted.




