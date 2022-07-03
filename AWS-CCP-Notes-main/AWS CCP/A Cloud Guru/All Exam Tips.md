# All Exam Tips

## Chapter 2 - Cloud Concepts & Technology

### [[Chapter 2 - Cloud Concepts & Technology|Chapter Start]]

### [[Chapter 2 - Cloud Concepts & Technology#Summary|Summary]]

## [[Chapter 2 - Cloud Concepts & Technology#What is Cloud Computing|What Is Cloud Computing?]]

- Know the Six Advantages
	- Trade Capital Expense for Variable Expense
	- Benefit from Massive Economies of Scale
	- Stop Guessing About Capacity
	- Increase Speed & Agility
	- Stop Spending Money Running & Maintaining Datacentres
	- Go Global in Minutes
- Know the 3 Types of Cloud Computing
	- Infrastructure as a Service (IAAS)
	- Platform as a Service (PAAS)
	- Software as a Service (SAAS)
- Know the 3 Types of Cloud Computing Deployment
	- Public
	- Private
	- Hybrid

## [[Chapter 2 - Cloud Concepts & Technology#Around the World with AWS|Around the World with AWS]]

- Understand the difference between region, AZ, and EL
	- Region is physical location consisting of two or more AZs
	- AZ is one or more discrete data centres
	- ELs are AWS endpoints used for caching
- Know how to choose the right region

## [[Chapter 2 - Cloud Concepts & Technology#Account Setup|Account Setup]]

- Just need to know the support plans
	- Basic, Developer, Business, Enterprise
	- Varying response times, prices, and levels of dedicated support/contacts
- Might be asked about Service Level Agreements e.g. response time

## [[Chapter 2 - Cloud Concepts & Technology#Billing Alarms|Billing Alarms]]

- Will be asked about 'automatic notifications' - just say to create CloudWatch alarm

## [[Chapter 2 - Cloud Concepts & Technology#Let's Start to Cloud Identity Access Management IAM|Identity Access Management (IAM)]]

- IAM is applied globally - not per region
- Know the different methods of accessing the console
	- Console
	- Programmatically (CLI)
	- SDK
- Root account has full administrator access
	- Should not be used
	- Should be secured with MFA
- Group - place to store users
	- Users automatically inherit from that group
	- To give permissions to a group, apply a policy to group (written in JSON)
- Easiest way to audit/export all users is via credential report
- Remember your best practices
	- Limit Root Account Usage
	- 1 User = 1 Human
	- Use Groups and Policies
	- Strong Password Policies
	- MFA wherever possible
	- Roles to Access Services
	- Access Keys for Programmatic Access
	- IAM Credential Reports

## [[Chapter 2 - Cloud Concepts & Technology#S3 101|S3 101]]

Oldest service
Secure, durable, highly-scalable object storage

- Object-based i.e. allows uploading files
- Not suitable for operating systems or non-flat files like databases
- Files can be 0 to 5 TB
- Unlimited storage
- Files stored in buckets
- S3 is a universal namespace
- All S3 buckets have a given URL
- Successful uploads get a HTTP 200 status code
- Key-value pairs in objects (name, bytes)
- Read After Write consistency for PUTS of new objects
- Eventual Consistency for overwrite PUTS and DELETES (can take some time to propagate, usually up to a second)
- Remember the [[Chapter 2 - Cloud Concepts & Technology#Storage Classes|storage classes]]

## [[Chapter 2 - Cloud Concepts & Technology#Creating an S3 Bucket|Creating an S3 Bucket]]

- Names must be globally unique and DNS compliant
- Buckets are viewed globally but can be situated in individual regions (for latency)
- Can use Cross-Region Replication to automatically replicate data from one region to another
- Can change storage classes and encryption of objects on the fly
- Restricting Bucket Access/Controlling permissions
	- Bucket policy applies to whole bucket
	- Object policies are per object
	- IAM policies can grant access to users and groups
- Allowing public access on bucket doesn't automatically make objects public - just means they *can* be public
- You cannot make an object public while public access is blocked

## [[Chapter 2 - Cloud Concepts & Technology#Creating a Serverless Static Website on S3|Creating a Serverless Static Website on S3]]

- Can make entire buckets public with bucket policies
- Use S3 to host static sites (HTML, CSS, Javascript)
	- No dynamic sites (databases etc)
- S3 scales automatically to meet demand

## [[Chapter 2 - Cloud Concepts & Technology#S3 Versioning|S3 Versioning]]

- Stores all versions of an object
	- All writes
	- All deletes
- Great backup tool
- Versioning cannot be disabled once enabled - only suspended
- Integrates with lifecycle rules - e.g. archive old version
- Can use versioning with MFA delete - prevents deletion without MFA

## [[Chapter 2 - Cloud Concepts & Technology#CloudFront|CloudFront]]

Amazon's Content Delivery Network (CDN)
System of distributed servers that delivers webpages and other web content to a user based on their geographical location, origin of the webpage, and a content delivery server

- EL - where it's cached (separate to region)
- Origin - origin of all files that CDN will distribute
- Distribution - name given to CDN (collection of ELs)
- Distribution types
	- Web distribution - used for websites
	- RTMP distribution - used for media streaming (adobe flash protocol)
- Edge Locations are not read only - can write to them too
	- For example, in transfer acceleration
- Objects cached for life of TTL
- Can clear cached objects, but this incurs a charge

## [[Chapter 2 - Cloud Concepts & Technology#EC2 101|EC2 101]]

Elastic Compute Cloud

- EC2 is web service that provides resizable compute capacity in cloud - essentially a virtual server in the cloud
- Reduces time required to obtain and boot new server instances - allows quickly scaling up and down
- 4 pricing models: on-demand, reserved, spot, and dedicated hosts
- Not charged for spot instances for partial hour if automatically terminated
- EC2 Instance Types - **FIGHTDRMCPXZAU** - See [[Chapter 2 - Cloud Concepts & Technology#EC2 Family Mnemonic|Mnemonic]]
- EBS is virtual disk in cloud - types include GP2, IO1, ST1 and SC1

## [[Chapter 2 - Cloud Concepts & Technology#Using EC2 Lab|Using EC2 Lab]]

- EC2 is compute based - it is not serverless, it's a server in the cloud!
- Connect to EC2 using private key
- Remember common ports: SSH, RDP, HTTP/S
- Security Group is essentially a virtual firewall
	- Let everything in: `0.0.0.0/0`
	- Let specific IP in: `a.b.c.d/32`
- Always design for failure - have one EC2 in each availability zone

## [[Chapter 2 - Cloud Concepts & Technology#Using the AWS Command Line|Using the AWS Command Line]]

3 ways to interact:
- Console
- CLI
- SDKs (beyond this course - uses programming language libraries)

## [[Chapter 2 - Cloud Concepts & Technology#Using Roles|Using Roles]]

- Roles are more secure than storing access keys on an EC2
- Easier to manage
	- Adding more policies to role updates instantly
- Can apply to instances at any time - change takes place immediately

## [[Chapter 2 - Cloud Concepts & Technology#Let's Use a Load Balancer|Load Balancers]]

- 3 types:
	- application - layer 7 aware, intelligent decisions
	- network - extreme performance, static IPs
	- classic - test & develop, keep costs low
- Keep EC2s in multiple AZs to have little to no outage
- Allows fault-tolerant architecture

## [[Chapter 2 - Cloud Concepts & Technology#Databases 101|Databases 101]]

**RDS** - Relational Database Service (SQL, used for OLTP)
Supports several engines:
- SQL
- MySQL
- PostgreSQL
- Oracle
- Aurora
- MariaDB

**DynamoDB** - Non-Relational (NoSQL)

**Redshift** - Data Warehousing Service (Used for OLAP)

**Elasticache** - For caching data (speeds up performance for frequent identical queries)

Not expected to know much about DDB, RS, EC besides use case - RDS requires a little more knowledge about practical use on exam

## [[Chapter 2 - Cloud Concepts & Technology#Buying a Domain Name|Buying a Domain Name]]

- Route53 is Amazon's DNS service
- It is global, similar to IAM and S3 - no region specified
- You can use it to direct traffic around world, and register domain names

## [[Chapter 2 - Cloud Concepts & Technology#Elastic Beanstalk|Elastic Beanstalk]]

Can quickly deploy and manage apps in cloud, without worrying about infrastructure that runs applications
- don't need to worry about provisioning EC2, installing PHP etc
- just upload application code, and EB handles the rest
- decides details of capacity provisioning, load balancing, scaling, and application health monitoring

## [[Chapter 2 - Cloud Concepts & Technology#Cloudformation|CloudFormation]]

- Helps you model and set up AWS resources
	- spend less time managing those resources
	- more time focusing on apps that run within AWS
- Create a template that describes all desired resources - EC2s, RDS, Lambda, VPCs, Subnets
	- CloudFormation takes care of provisioning and configuring resources
	- Handles all dependencies
- EB and CF are both free - but the resources they provision *are not*
- EB is limited in what it can provision and is not programmable - CF can provision almost any service and is fully programmable

## [[Chapter 2 - Cloud Concepts & Technology#Global AWS Services|Global Services]]

- IAM
- Route 53
- CloudFront
- SNS
- SES

## [[Chapter 2 - Cloud Concepts & Technology#Services that can be Used On Premise|On-Prem Services]]

- Snowball
- Snowball Edge
- Storage Gateway
- CodeDeploy
- Opsworks
- IoT Greengrass

## [[Chapter 2 - Cloud Concepts & Technology#CloudWatch 101|CloudWatch 101]]

- Used for monitoring performance
- Can monitor most of AWS
- Can also monitor apps running on AWS
- Can setup custom metrics e.g. number of visitors on site, number of active database connections
- CloudWatch EC2 monitors every 5 minutes by default - 1 minute intervals by turning on detailed monitoring
- Can create CloudWatch alarms that trigger notifications

## [[Chapter 2 - Cloud Concepts & Technology#AWS Systems Manager|Systems Manager]]

- Can be used to manage fleets of EC2 instances and VMs
- Piece of software installed on each VM
- Can be both inside AWS and on-premise
- Run Command used to install, patch, uninstall software
- Integrates with CloudWatch to give dashboard of entire estate

## [[Chapter 2 - Cloud Concepts & Technology#Service Health Dashboard|Service Health Dashboard]]

- Just need to know that this is the method used if asked about how you can view an outage based on service
- Also like to confuse you with personal health dashboard

## [[Chapter 2 - Cloud Concepts & Technology#Personal Health Dashboard|Personal Health Dashboard]]

Remember difference:
- service health dashboard shows all services
- personal health dashboard just shows services you use

## [[Chapter 2 - Cloud Concepts & Technology#S3 vs EBS vs EFS|S3 vs EBS vs EFS]]

Scenario-based questions on exam - test you on which storage medium you should use

Storing objects/files -> think S3
Storing OS/DB -> think EBS

- S3: flat files - pictures, docs, videos - not operating systems, databases
- EBS: virtual disk attached to EC2 - can store non-flat files - size can change, but not automatically - can attach to multiple instances now, but once couldn't
- EFS: virtual disk attached to EC2 - can be attached to multiple instances - size is elastic, scales up and down

## [[Chapter 2 - Cloud Concepts & Technology#Global Accelerator|Global Accelerator]]

- Know what it is and where you'd use it
	- create accelerators to improve performance
	- for global apps
- Routes via AWS backbone, not the internet
- Up to 60% performance increase
- Scenario-based questions about increasing reliability/consistency when internet congested -> think Global Accelerator

## Chapter 3 - Billing & Pricing

### [[Chapter 3 - Billing & Pricing|Chapter Start]]

### [[Chapter 3 - Billing & Pricing#Billing Pricing Summary|Summary]]

## [[Chapter 3 - Billing & Pricing#AWS Pricing 101|AWS Pricing 101]]

- Remember Fundamental Principles (you pay as you go, pay for what you use, pay less as you use more, pay even less when you reserve capacity)
- Remember Capex vs Opex
	- Capex is up front, fixed sunk cost
	- Opex is where you pay for what you use
- Remember EC2 pricing models (on-demand, reserved, spot, dedicated)
- Remember free services (VPC, Elastic Beanstalk, CloudFormation, IAM, Auto Scaling, Opsworks, Consolidated Billing) - remember resources provisioned are not free
- Read "How AWS Pricing Works" Whitepaper

### Various Pricing Stats

**Free Usage Tier**

- Can run a free EC2 micro instance for a whole year
- Free usage tier for S3, EBS, ELB, AWS Data transfer, and other services

**EC2 Pricing**

- Standard monitoring is every 5 minutes - detailed monitoring is every 1 minute and increases the price
- Spot instances - you are charged if you cancel your spot instance yourself, but you're not charged for a partial hour of usage if Amazon cancel your instance

**Lambda Pricing**

- Free tier provides 1 million requests per month, $0.20 / 1 million requests thereafter (price may have changed)
- 400,000 GB-seconds per month free, up to 3.2 million seconds of compute time - $0.00001667 for every GB-second used thereafter

**Snowball Pricing**

- Per-job fee: $200 for 50 TB, $250 for 80 TB
- First 10 days of transfer are free, $15/day thereafter

## [[Chapter 3 - Billing & Pricing#AWS Budgets vs Cost Explorer|AWS Budgets vs Cost Explorer]]

- Know the difference between the two:
	- AWS Budgets lets you forecast and monitor costs **before** incurred
	- Cost Explorer lets you analyse costs **after** incurred

## [[Chapter 3 - Billing & Pricing#AWS Support Plans|AWS Support Plans]]

- What level has a TAM? **Enterprise**
- Know response times - what levels you need for `X` minutes response time
- *All* accounts receive billing support

## [[Chapter 3 - Billing & Pricing#Tagging Resource Groups|Tagging & Resource Groups]]

What are tags?
- key value pairs attached to AWS resources
- Metadata
- Tags can sometimes be inherited

Resource groups make it easy to group resources using tags assigned to them
- can group resources that share one or more tags (for example, region, name, health checks etc)
- using resource groups you can apply automation to resources tagged with specific tags
- resource groups in combination with AWS systems manager allow you to control and execute automation against entire fleets of EC2 instances, at the push of a button
- Resource groups are regional

Tag editor is a global service
- allows us to discover resources and add additional tags to them
- newer regions may take time to become compatible with tag editor

## [[Chapter 3 - Billing & Pricing#AWS Organisations Consolidated Billing|AWS Organisations & Consolidated Billing]]
2 flavours
- full access (organisational units, accounts behind OUs, can apply policies to OUs and accounts)
- consolidated billing only - just uses the billing features

Best practices with organisations:
- enable MFA on root account
- strong and complex password
- paying account used for billing only
- use CloudTrail to collect logs from other accounts; feed into separate logging account

Linked accounts
- 20 linked accounts max
- Add more - contact AWS

Consolidated billing:
- allows you to get volume discounts on all accounts
- unused reserved instances for EC2 are applied across the group

Billing alerts
- when monitoring enabled on paying account, billing data for all linked accounts included
- can still create billing alerts per individual account

CloudTrail:
- way of auditing what people are doing within AWS
- works on per-account, per-region basis
- can consolidate logs in one bucket - turn CloudTrail on in root/logging/paying account, create bucket with cross-account access policy, turn CloudTrail on in other accounts and log to bucket

Practical lab:
- Organisations allows building OUs and attaching accounts to these
- Can create policies - can be applied directly to OUs and all accounts will inherit, or apply directly to an account

## [[Chapter 3 - Billing & Pricing#AWS Quick Starts AWS Landing Zones|AWS Quick Starts AWS Landing Zones]]

Know the difference:
- Quickstart is way of deploying environments quickly, using CloudFormation templates built by AWS Solutions Architects who are experts in that particular technology
- Landing Zone is solution that helps customers quickly setup a secure, multi-account AWS environment based on AWS best practices

## [[Chapter 3 - Billing & Pricing#Different AWS Cost Calculators|Different AWS Cost Calculators]]

- Simple Monthly Calculator used to calculate running costs on per-month basis - not a comparison tool
- TCO used to compare costs of running infrastructure on premise vs in the AWS Cloud - will generate reports that you can give to C-level execs to make a business case to move to the cloud
- They supposedly come up a lot - but TCO seems to have been retired/replaced

## Chapter 4 - Security in the Cloud

### [[Chapter 4 - Security In The Cloud|Chapter Start]]

### [[Chapter 4 - Security In The Cloud#Summary|Summary]]

## [[Chapter 4 - Security In The Cloud#Shared Responsibility Model|Shared Responsibility Model]]

- AWS responsible for security **of** the cloud
	- hardware, underlying OS, global infrastructure
	- software sitting on those stacks e.g. virtualisation software, SQL server on RDS
- Customer responsible for security **in** the cloud
	- encrypting data at rest and in transit
	- your own operating systems when it comes to EC2
	- your security groups, networks, firewall configs
	- IAM, customer data

Will come up a lot - visualise what the question is asking:
- can *you* do this in the AWS console/inside EC2?
- if yes, you are probably responsible - SGs, IAM users, patching EC2 OS or databases running on EC2 etc
- if not, AWS is probably responsible - datacentres, security cameras, cabling, patching RDS operating systems etc
- encryption is a shared responsibility - S3 object, AWS do the encryption and store the keys - but you are the one who has to turn the encryption on, and make sure it's encrypted in transit - if providing own key, then it's your responsibility

## [[Chapter 4 - Security In The Cloud#AWS WAF AWS Shield|AWS WAF & AWS Shield]]

- WAF designed to stop hackers doing things like XSS on application layer
- AWS Shield is a DDoS mitigation service designed to stop DDoS attacks

## [[Chapter 4 - Security In The Cloud#AWS Inspector vs AWS Trusted Advisor vs CloudTrail|Inspector vs Trusted Advisor vs CloudTrail]]

Inspector
- runs at OS-level on EC2
- used for inspecting EC2 instances for vulnerabilities

Trusted Advisor
- runs across whole AWS account
- more than just security checks - cost optimisation, performance, fault tolerance

CloudTrail
- operates across AWS account
- logs API calls and their source account, user and IP
- increases visibility into user and resource activity

## [[Chapter 4 - Security In The Cloud#AWS KMS vs HSM|AWS KMS vs HSM]]

- **AWS KMS** is Amazon's encryption, decryption, and key management service - it runs on shared hardware
- **CloudHSM** does pretty much everything KMS does, but uses dedicated hardware - better for compliance

## [[Chapter 4 - Security In The Cloud#Parameter Store vs Secrets Manager|Parameter Store vs Secrets Manager]]

Both places to store passwords

- **Parameter Store** is free, but limited to 10,000 parameters - can be encrypted
- **Secrets Manager** does everything Parameter store does with no limit (but costs money) - can also generate random passwords and automatically use service passwords when integrated with CloudFormation

## [[Chapter 4 - Security In The Cloud#Athena vs Macie|Athena vs Macie]]

- Athena: interactive query service
	- queries data in S3 using standard SQL
	- serverless
	- commonly used to analyse log data
- Macie: auditing/security tool for identifying and protecting PII in S3
	- can also analyse CloudTrail logs for suspicious API activity
	- interactive dashboards, reports and alterting
	- great for PCI-DSS compliance

## [[Chapter 5 - Advanced AWS Concepts#Different Compute Services|Different Compute Services]]

Full list of compute services that might come up on the exam:
1) EC2 - virtual machine in the cloud
2) Lightsail - simple cloud servers - EC2 you deploy into a VPC (virtual datacentre in cloud, you can control all firewall rules and integrate services etc), Lightsail is much simpler (you pick the type of VM you want, choose the size, and it deploys it for you - little customisation but good way of getting started)
3) Lambda - serverless compute in the cloud
4) Batch - compute service for batch computing
5) Elastic Beanstalk - PAAS compute service - provisions web and database servers, installs MySQL, lets you deploy quickly to cloud
6) Serverless Application Repository - allows you to deploy pre-provisioned serverless applications (e.g. Alexa skills) - can deploy into Lambda and edit code
7) AWS Outposts - way of extending compute to your own data centers or on-premises
8) EC2 Image Builder - helps you build your own custom EC2 images for Linux and Windows
9) AWS App Runner - fully managed containerised web application/API service

## [[Chapter 5 - Advanced AWS Concepts#Lambda|Lambda]]

- Lambda **scales out** (not up) automatically
- Lambda functions are independent (1 event = 1 function)
- Lambda is serverless
- Know how Lambda is priced (per invocation and per execution time)
- You can have multiple versions of your code inside Lambda
- Understand shared responsibility model - you are responsible for your code and the version of the language it runs on, Amazon for everything else