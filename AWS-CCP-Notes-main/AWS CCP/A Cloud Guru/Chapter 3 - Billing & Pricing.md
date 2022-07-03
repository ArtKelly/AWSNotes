# Chapter 3 - Billing & Pricing

## AWS Pricing 101

Say worth 12%, more like 25%

Fundamental Principles:
- you pay as you go
- you pay for what you use
- you pay less as you use more
- you pay even less when you reserve capacity

### Exam Tips

- Remember Fundamental Principles (you pay as you go, pay for what you use, pay less as you use more, pay even less when you reserve capacity)
- Remember Capex vs Opex
	- Capex is up front, fixed sunk cost
	- Opex is where you pay for what you use
- Remember EC2 pricing models (on-demand, reserved, spot, dedicated)
- Remember free services (VPC, Elastic Beanstalk, CloudFormation, IAM, Auto Scaling, Opsworks, Consolidated Billing) - remember resources provisioned are not free
- Read "How AWS Pricing Works" Whitepaper

### Different Pricing Models

#### Capex vs Opex

- Capex stands for Capital Expenditure - pay up front - fixed, sunk cost
	- Difficult for startups
	- Need investors to even get the ball rolling
- Opex stands for Operational Expenditure - pay for what you use - comparable to utility bills
	- Startups can use to scale out - only pay when people start visiting your website

### Pricing Policies

**Basic Policies**

- Pay as you go
- Pay less when you reserve
- Pay even less per unit by using more
- Pay even less as AWS grows
- Custom pricing

**Key Principles**

Pricing models vary across services, but important to review key principles and best practices that are broadly applicable

- Understand the Fundamentals of Pricing
- Start early with cost optimisation
- Maximise power of flexibility
- Use the right pricing model for the job

#### Understand the Fundamentals of Pricing

3 fundamental drivers of cost:
- Compute
- Storage
- Data Outbound (not data entering in)

#### Start Early with Cost Optimmisation

Not just tech evolving - requires organisations changing how they operate
Move from IT being treated as periodic capital investment -> world where pricing closely tied to efficient use of resources
Pays to understand what drives cloud pricing and build strategy to optimise it
When comes to understanding pricing and optimising costs, never too early to start
Easiest to put cost visibility and contro mechanisms in place before environment grows large and complex (spirals out of control)
Managing cost-effectively from the start ensures managing cloud doesn't become an obstruction as you grow and scale

TLDR:
- put effort in to optimising your cost as early as possible
- add visibility of costs
- add control mechanisms (billing alarms)
- prevents cost spiralling out of control


#### Maximise Power of Flexibility

Services priced independently and transparently
Can choose and pay for exactly what you need, and no more
No minimum commtiments/long-term contracts required (unless choosing to save money via reservation model)
By paying on as as-needed basis, can redirect focus to innovation and invention
Reduced procurement complexity, enables business to be fully elastic

Don't pay for resources when not running
By turning off instances you don't use, can reduce costs >= 70% compared to using 24/7
Enables cost-efficiency while at same time having all power you need when workloads are high
Only use environment when you need it

#### Using Right Pricing Model for the Job

Several models based on product, including:
- on demand
- dedicated
- spot
- reservations

Also offers **free usage tier** to get started in cloud
- Can run a free EC2 micro instance for a whole year
- Free usage tier for S3, EBS, ELB, AWS Data transfer, and other services

#### Free Services

Following services are **free** by default:
- Amazon VPC (virtual datacentre in cloud - where machines live - more details in solutions architect)
- Elastic Beanstalk (but resources it provisions are not free)
- CloudFormation (but resources it provisions are not free)
- IAM
- Autoscaling (but resources it provisions are not free)
- Opsworks (but resources it provisions are not free)
- Consolidated Billing

#### EC2 Pricing

What determines price?
- Clock hours of server time - i.e. either /second or /hour
- Instance type (`t` family priced differently to `r` family)
- Pricing model (reserved/spot/on demand)
- Number of instances
- Load Balancing (network load balancing > classic load balancing)
- Detailed monitoring (standard cheaper, detailed monitors every 1 minute and is more expensive)
- Autoscaling (more instances, more money)
- Elastic IP addresses
- Operating systems and software packages (Windows > Linux)

Models:
- On demand: fixed rate by hour (or second) with no commitment
- Reserved: capacity reservation, significant discount
- Spot: bid whatever price you want for spare instance capacity, greater savings if application has flexible start/end times e.g. batch processing late at night (not good if always running)
- Dedicated host: physical EC2 dedicated for you (good for server-bound software licesnses)

Reserved Instances:
- Reserve capacity, receive discount on instance usage compared to on-demand
- More you pay up front + longer contract term, more you save

![[Pasted image 20210514093403.png]]


#### Lambda Pricing

Serverless way of doing compute - S3 is serverless, so is Lambda
Explored in more detail in Solutions architect
Alexa uses Lambda
Executes for ~0.5 seconds - not running an EC2 to run this, just paying for that half a second

**What determines price?**

- Request Pricing (how many calls)
	- Free Tier: 1 million requests per month (very generous)
	- $0.20 per 1 million requests thereafter
- Duration Pricing (how long excecuted for)
	- 400,000 GB-seconds (memory allocated to task per second that task runs) per month free, up to 3.2 million seconds of compute time
	- $0.00001667 for every GB-second used thereafter
- Additional charges
	- May incur additional charges if Lambda uses other services or transfers data (e.g. if function reads/writes to S3, charged for that)

#### EBS Pricing

**What determines price?**

- Volumes (Per GB)
- Snapshots (Per GB)
- Data Transfer

#### S3 Pricing

**What determines price?**

- Storage Class
- Storage itself (GB)
- Requests (GET, PUT or COPY)
- Data Transfer

#### Glacier Pricing

**What determines price?**

- Storage
- Data Retrieval Time (longer is cheaper)

![[Pasted image 20210514094203.png]]

#### Snowball Pricing

PB-scale data transport solution
Secure aplicances to transfer large amounts of data in and out of cloud - gigantic disk, data transferred locally and shipped to datacentre

**What determines price?**

- Service Fee per job
	- Snowball 50 TB: $200
	- Snowball 80 TB: $250
- Daily Charge
	- First 10 days are free, after that $15/day
- Data Transfer
	- Transfer -> S3 free, transfer out is not (want you to stay in cloud)


#### RDS Pricing

**What determines price?**

- Clock hours of server time
- Database Characteristics (i.e. what engine)
- Database Purchase Type (i.e. instance size)
- Number of Database Instances
- Provisioned Storage (i.e. size in GB)
- Additional Storage
- Requests
- Deployment Type
- Data Transfer

#### DynamoDB

**What Determines Price?**

- Provisioned Throughput (Write)
- Provisioned Throughput (Read)
- Indexed Data Storage (amount stored inside DB)

![[Pasted image 20210514094952.png]]

#### CloudFront

**What Determines Price?**

- Traffic Distribution
- Number of Requests
- Data Transfer Out

## AWS Budgets vs Cost Explorer

### Exam Tips

- Know the difference between the two:
	- AWS Budgets lets you forecast and monitor costs **before** incurred
	- Cost Explorer lets you analyse costs **after** incurred

### AWS Budgets

- Gives you ability to set custom budgets
- Alerts when costs/usage exceed (or are forecasted to exceed) budgeted amount
- Used to budget and forecast costs *before* they've been incurred

### AWS Cost Explorer

- The opposite - easy to use interface that lets you visualise, understand, and manage AWS costs and usage over time
- Used to explore costs *after* they've been incurred

### In the Console

Account Dropdown > Billing Dashboard
Budgets > Create a Budget
Cost Explorer needs to be enabled to be used

## AWS Support Plans

### Exam Tips

- What level has a TAM? **Enterprise**
- Know response times - what levels you need for `X` minutes response time
- *All* accounts receive billing support

### Summary

||Basic|Developer|Business|Enterprise|
|---|---|---|---|---|
|**Cost**|FREE|$29/month|$100/month|$15,000/month|
|**Tech Support**|None|Business hours access via email|24x7 email + phone|24x7 email + phone|
|**TAM**|NO|NO|NO|YES|
|**Who can open cases?**|None|1 person, unlimited cases|Unlimited contacts, unlimited cases|Unlimited contacts, unlimited cases|
|**Case Severity / Response Times**|None|**General Guidance:** < 24 business hours - **System Impaired:** < 12 business hours|**General Guidance:** < 24 hours - **System Impaired:** < 12 hours - **Production System Impaired:** < 4 hours - **Production System Down:** < 1 hour|**General Guidance:** < 24 hours - **System Impaired:** < 12 hours - **Production System Impaired:** < 4 hours - **Production System Down:** < 1 hour - **Business-critical System Down:** < 15 minutes|

## Tagging & Resource Groups

### Exam Tips

What are tags?
- key value pairs attached to AWS resources
- Metadata
- Tags can sometimes be inherited

Resource groups make it easy to group resources using tags assigned to them
- can group resources that share one or more tags (for example, region, name, health checks etc)
- using resource groups you can apply automation to resources tagged with specific tags
- resource groups in combination with AWS systems manager allow you to control and execute automation against entire fleets of EC2 instances, at the push of a button

Tag editor is a global service
- allows us to discover resources and add additional tags to them
- newer regions may take time to become compatible with tag editor

Resource groups are regional

### What are Tags?

Key-value pairs attached to AWS resources
Contain metadata
Tags can sometimes be inherited - for example, attach tag to a stack - provisioned resources will inherit that tag

Can contain specific info:
- EC2 - Public & Private IP Addresses
- ELB - Port Configurations
- RDS - Database engine
- etc...

### Resource Groups

Make it easy to group your resources using tags that are assigned to them. Can group resources that share one or more tags.

Can contain info such as:
- Region
- Name
- Employee ID
- Department

### In the Console

Resource Groups in top Navbar
\> Create a group
\> Tag editor

- Provision some instances
	- Add some tags
		- Name: Webserver01
		- Department: Finance
		- Region: N. Virginia
		- EmployeeID: 9684984541
	- Select standard SGs, launch
	- Repeat three times, change region tag for each

Tag editor:
- select regions to tag (not all regions will be available straight away)
- select resource types (can select all)
- sort by Tags - dropdown e.g. Department
- provide a search term
- find resources > shows all tagged resources
- can then click and see all other tags
- click manage resources > EC2 screen

Tag editor is a **global** service

Create resource group:
- create query-based group
- this **is** regional - create group in a region
- select tag based
- can select resource types
- can add tags
- add group details e.g. 'Department - Stockholm'

Execute Automation:
- Systems manager lets you manage at scale
- Can click a command - e.g. `AWS-StopEC2Instance`
- Run it against the resource group
	- Run entire automation at once
	- Targets > Resource Group > Paste Name (Department - Stockholm)
	- Select Parameter - Instance ID
	- Execute Automation

## AWS Organisations & Consolidated Billing

### Exam Tips

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

### What is AWS Organisations?

Account management service - enables you to consolidate multiple AWS accounts into an organisation that you create and centrally manage

Two feature sets:
- consolidated billing
- all features

Why need multiple AWS accounts?
- maybe org with 20 devs each with an account
- or might have a production account with certain architecture, then an account for testing and training

Structure:
- Root account
- Organisational Units - could be prod, dev etc
- AWS accounts within OUs
- Can apply policies to OUs - e.g. prevent a dev account from provisioning EC2s

![[Pasted image 20210517102025.png]]

OUs turned on, benefit from economies of scale
The more you use, the less you pay
Cheaper rates with consolidated billing

This is with full features
Can turn orgs on and just have consolidated billing:
- paying account
- linked accounts - produce monthly bill
- paying account pays bills
- it's independent, cannot access resources of other accounts e.g. turn off EC2s, block provisioning resoruces
- all linked accounts are independent from each other
- currently a limit of 20 linked accounts for consolidated billing - soft limit

![[Pasted image 20210517102108.png]]

Advantages:
- one bill per AWS account
- easy to track what accounts are spending - track charges, allocate costs
- volume pricing discount

For example, S3 tiered pricing - more you use, cheaper it gets
Never be asked about specific pricing in an exam - will always change

### Consolidated billing Practical Example

#### With S3

Using S3 Tiered Pricing:

![[Pasted image 20210517101736.png]]

Small saving - but that's just for one service

![[Pasted image 20210517102208.png]]

#### With EC2

Test/dev uses 6 on-demand
Prod has 5 reserved instances, but only uses 3 - assume max discount from upfront
Assume using same EC2 instance type
Will be billed for all 5 reserved instances (paid for), but only billed for 4 reserved - you get to use the discount from the reserved instances in another account

![[Pasted image 20210517102312.png]]

### What is CloudTrail?

CloudTrail vs CloudWatch
- CloudWatch monitors performance - e.g. EC2 - maybe it triggers a warning when usage goes above 80% for 5 minutes, it provisions another
- CloudTrail monitors API calls in the AWS platform - used for auditing - when making changes to AWS environment
- Basically performance & resources vs. making changes

### Best Practices with AWS Organisations

- always use MFA on root account
- always use a strong and complex password on root account
- paying account should be used for billing purposes only - don't provision resources in it

#### Using CloudTrail with AWS Organisations

- Per AWS account, enabled per region
- Consolidate logs into an S3 bucket:
	- turn on CloudTrail in paying account
	- create bucket policy that allows cross-account access + create bucket in paying account
	- Turn on CloudTrail in all other accounts and use bucket in the paying account - push out cloudtrail logs from all other accounts into S3 in paying account

Gives you a log of what everyone is doing
If someone deletes something in an account, they can't delete it from the logs - all in centralised account
Absolute best practice is an entirely separate logging account
Accounts can only write to bucket, not read
Complete source of truth, can't make changes

## AWS Organisations Lab

### Exam Tips

- Organisations allows building OUs and attaching accounts to these
- Can create policies - can be applied directly to OUs and all accounts will inherit, or apply directly to an account

### Lab

Account Dropdown > My Organisations

Global Service

Create Organisation:
- single payer and centralized cost tracking
- create and invite accounts
- allows you to apply policy-based controls
- helps you simplify organisation-wide management of AWS sevices

OR create an organisation with only consolidated-billing features

Create one with full access:
- verify email
- invite/create additiona accounts
	- invite by email/account ID + add a note

Create an OU:
- give it a name e.g. Devs, HR, Sales

Policies > Create Policy
- FullAWSAccess policy provided by default
- Can create new one e.g. `LetsGoServerless`
	- Description: "Policy blocks EC2"
	- Choose overall effect (`Deny`/`Allow`)
	- Statement Builder > Select Service > Select Action
		- Can be a specific action e.g. `AssignIpv6Addresses`, or click `Select All`
	- Click `Add statement`
	- Click `Create policy`

Select A

Select accounts + add to OUs:
- select account > `Move` > Group Name
- Clicking developers OU will show accounts

To view policies, click `Service control policies` (SCP)
- policies are inherited by default e.g. `FullAWSAccess`
- Click `Attach` to add `LetsGoServerless`

Root account cannot invite another root account

## AWS Quick Starts & AWS Landing Zones

### Exam Tips

Know the difference:
- Quickstart is way of deploying environments quickly, using CloudFormation templates built by AWS Solutions Architects who are experts in that particular technology
- Landing Zone is solution that helps customers quickly setup a secure, multi-account AWS environment based on AWS best practices

### Quickstart

`https://aws.amazon.com/quickstart`

![[Pasted image 20210517104132.png]]

Broken down into different services:
- machine learning
- IoT
- data lakes
- blockchain

All environments created by solution architects
get started with certain techs very quickly
For example, start a Microsoft Exchange Server

![[Pasted image 20210517104205.png]]

To start:
- view guide
- click `launch quickstart for a new VPC`
- brings you to CloudFormation - uses a CF template
- view/edit in designer - see what it's building
	- for example, Active Directory Stack + Exchange Server Stack
	- combines several stacks
	- beyond scope to understand stack, but know it exists

Deploys solutions into your account
Solutions built by AWS experts in that tech

Completely free to use - but like anything, resources provisioned you must pay for

### Landing Zone

`https://aws.amazon.com/answers/aws-landing-zone` -> `https://aws.amazon.com/solutions/implementations/aws-landing-zone/`

Where Quickstart will provision resources in an account via CF, Landing Zone lets you setup multi-account environment at click of button

![[Pasted image 20210517104016.png]]

Deploys 4 accounts, sets them up
Automates multi-account setups
Released in 2018 - may or may not come up

## AWS Partner Program

Two types of partner:
- consulting - these partners provide a service - design, architect, build, migrate, and manage customer workloads and applications on AWS - service based, consulting based
- technology - provide hardware, connectivity, software solutions either hosted on, or integrated with, AWS cloud

How to be a consulting partner?
- need certain number of people in organisation
- three tiers

|Partner|No. Practitioner Certs|No. Associate Certs|No. Professional/Specialty Certs|
|---|---|---|---|
|Select|2|2|2|
|Advanced|4|4|6|
|Premier|10|10|10|

Employee with both CCP, Solutions Architect, and Solutions Architect Professional - take up one slot from each of tiers (one employee can count towards multiple certificates)

Means your certificate counts towards organisation becoming a partner - incentivises exams

## Different AWS Cost Calculators

### Exam Tips

- Simple Monthly Calculator used to calculate running costs on per-month basis - not a comparison tool
- TCO used to compare costs of running infrastructure on premise vs in the AWS Cloud - will generate reports that you can give to C-level execs to make a business case to move to the cloud
- They supposedly come up a lot - but TCO seems to have been retired/replaced

### Overview

Calculate costs using a couple of different calculators

Two feature sets:
- AWS simple monthly calculator - hosted static on S3, allows you to build out an AWS environment spec - number of instances, pricing plan, instance types etc - outputs an estimated monthly cost
- AWS total cost of ownership calculator - what is it costing you to have servers on-prem vs in cloud - give no. of servers and amount of storage, compares cost in-house/with AWS

TCO is a comparison, simple calculator is predicting cost

### Simple Monthly Calculator

[https://calculator.s3.amazonaws.com/index.html](https://calculator.s3.amazonaws.com/index.html)

Add resources/services:
- compute
- billing option
- estimates monthly bill

![[Pasted image 20210517115524.png]]

Seems to be being deprecated

### Total Cost of Ownership Calculator

[https://aws.amazon.com/tco-calculator/](https://aws.amazon.com/tco-calculator/)

Summarises pricing benefits - pay as you go etc
- allows estimating cost savings
- allows producing reports to present to boards etc to sell AWS to CTO
- save x% a year, 3-year total savings
- what's cost of transition?

To estimate:
- select currency
- on-prem/colocation (where renting a rack)
- select region
- select servers (name, number of processers, number of servers, amount of RAM, DB engine)
- select storage e.g. 500 TB of SAN SSD
- click calculate TCO

Tells you x% a year
Three year total savings

![[Pasted image 20210517115255.png]]

Shows you estimated environment:

![[Pasted image 20210517115327.png]]

Breaks down categories:

![[Pasted image 20210517115339.png]]

Can change and view assumptions in calculations section
Download Report button @ atop

Server costs, storage costs, network costs, all other overheads

![[Pasted image 20210517115403.png]]

### AWS Pricing Calculator (New)

[https://calculator.aws/#/](https://calculator.aws/#/)

TCO Link has expired - currently, AWS seems to offer a calculator based on adding resources you may need instead:

![[Pasted image 20210517115658.png]]

Add and configure a number of services:

![[Pasted image 20210517115741.png]]

![[Pasted image 20210517115819.png]]

![[Pasted image 20210517115905.png]]

![[Pasted image 20210517115917.png]]

## Billing & Pricing Summary

While number and types of services offered have increased dramatically, philosophy on pricing not changed:
- pay as you go
- pay for what you use
- pay less as you pay more
- pay even less when you reserve capacity

### Capex vs Opex
- Capex = Capital Expenditure - paid up front - fixed, sunk cost
- Opex = Operational Expenditure - pay for what you use

### EC2 Pricing Models
- On-demand (fixed rate, no commitment)
- Reserved (capacity reservation at significant discount)
- Spot (pay for spare capacity, not charged for partial hour of usage if cancelled)
- Dedicated Host (you and you only, save by using server-bound licenses)

### Free Services
- VPC
- Elastic Beanstalk
- CloudFormation
- IAM
- Auto Scaling
- Opsworks
- Consolidated Billing

(resources provisioned by free services are not free)

### Cost analysis

- AWS Budgets - predicts costs **before** incurred
- AWS Cost Explorer - analyses costs **after** incurred

### Support Plans
- Basic (free)
- Developer (>= $29/month)
- Business (>= $100/month)
- Enterprise (>= $15,000/month - only one with a TAM)

### Tags
- key-value pairs (metadata) attached to AWS resources
- can be inherited (e.g. via a tag on a CF template)
- Tag Editor is Global service that allows us to discover resources and add additional tags to them (newer regions may take some time to become compatible)

### Resource groups
- group resources using tags assigned
- group resources sharing one or more tags
- can apply automation to resources within a resource group using Systems Manager

### Organisations
- either full access (with root acc, OUs, policies) or just with consolidated billing (paying account)
- best practices include using MFA, strong and complex password, using paying account for billing only
- linked accounts: 20 only (soft limit)
- billing alerts: if monitoring enabled on paying account, billing data for all linked accounts is included - but you can still create individual account billing alerts
- CloudTrail: per-AWS account, enabled per region - enable in all regions, consolidate in a logging account (using bucket with cross-account policies)
- consolidated billing allows you to get volume discounts on all accounts - unused reserved instances for EC2 are applied across the group (if instance type matches)

### Quickstart
- way of deploying environments quickling using CF templates built by AWS Solutions Architects who are experts in that technology
- per-account

### Landing Zone
- helps customers setup a secure, multi-account AWS environment based on best practices
- currently does AWS Organisations Account, Shared Services Account, Log Archive Account, Security Account

### Calculators
- AWS Simple Monthly Calculator used to calculate monthly running costs (not a comparison tool)
- AWS TCO Calculator used to compare costs of running infrastructure on cloud vs on-prem - generates reports which can give to execs for business case (use if asked about a comparison)
- Calculators come up frequently