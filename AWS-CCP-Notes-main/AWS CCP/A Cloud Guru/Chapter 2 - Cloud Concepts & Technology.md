# Chapter 2 - Cloud Concepts & Technology

## What is Cloud Computing?

All it is is renting someone's computer

Basic applications
- Compute
- Database
- Storage
- Applications
- Other IT services

### Exam Tips

- Know the Six Advantages
- Know the 3 Types of Cloud Computing
- Know the 3 Types of Cloud Computing Deployment

### Six Advantages of Cloud

1) Trade Capital Expense for Variable Expense
	- Don't have to invest heavily in building data centres and wait for it to be setup
	- Pay as you go
		- No contracts
		- Stop paying as soon as you're done
2) Benefit from Massive Economies of Scale
	- You will never have the same purchasing power as Amazon
	- They pass those cost savings down
3) Stop Guessing About Capacity
	- Too much - wasted money
	- Too little - downtime
	- With Cloud you can setup metrics and autoscale
4) Increase Speed & Agility
	- Serverless architecture
	- Build quicker and cheaper
	- Not bogged down by setting up infrastructure before you can get started with development
5) Stop Spending Money Running & Maintaining Datacentres
	- Focus on what you're good at - your business itself
	- Don't focus on managing infrastructure - let someone else do that for you
6) Go Global in Minutes
	- Easily deploy in multiple regions in just a few clicks
	- Provide lower latency and better experience at minimal cost


### 3 Types of Cloud Computing

#### Infrastructure as a Service (IAAS)

- AWS is an example of this - specifically EC2
- You manage server and operating system
- Datacentre Provider will have no access to server itself

#### Platform as a Service (PAAS)

- For example GoDaddy - upload website code, and it points domain to it
- Don't manage hardware and infrastructure, operating systems
- Focus on your application - someone else manages security patches, updates, maintenance
- AWS offer this with [[Summary of Services#Elastic Beanstalk|Elastic Beanstalk]], [[Summary of Services#Lightsail|Lightsail]]

#### Software as a Service (SAAS)

- For example Gmail - you manage your inbox and nothing else
- Google handles data centers, servers, networks, storage, maintenance, patching

### 3 Types of Cloud Computing Deployment

**Public**
- AWS, Azure, GCP

**Hybrid**
- Mix of public and private
- Websites on public, confidential stuff on own servers

**Private**
- Completely on-premise
- All managed in own datacentre
- E.g. Open stack, VMWare, HyperV

### High Level Services

- AWS Global Infrastructure - their underlying datacentres
- A huge number of services and categories - you don't need to know them all!
- Key categories you need to know:
	- Cost Management (\*)
	- Security, Identity & Compliance (\*)
	- Migration & Transfer
	- Network & Content Delivery
	- Compute (\*)
	- Storage (\*)
	- Databases (\*)

### Public Cloud Market

- Constantly Growing
- 2019 AWS had 47% share
- Certs make you very employable
- Associate Courses - Certified Solutions Architect

## Around the World with AWS

### Exam Tips

- Understand the difference between region, AZ, and EL
	- Region is physical location consisting of two or more AZs
	- AZ is one or more discrete data centres
	- ELs are AWS endpoints used for caching
- Know how to choose the right region

### Availability Zones

Think of an AZ as a datacentre
Building filled with servers, storage arrays, load balancers
Redudant power, networking & connectivity
May be several datacentres but counted as one AZ

### Regions

Geographical Areas
2 or more AZs

E.g. in North America:
- US East, US West etc..
- GovCloud - locked down to Green Card holders
- etc

### Edge Locations

Endpoints for AWS
These cache content using Cloudfront Content Delivery Network (CDN)

More Edge Locations than regions

First time a file is accessed, it is downloaded directly
Next time you or someone else in your area accesses that file, they download it instead from a caching server (EL) in that area

### Choosing the Right Region

Things to consider:
- Data sovereignty laws
	- Can data only reside in a specific country?
- User latency
	- Where is majority of end users?
- AWS Service availability
	- Not all are available in every region
	- US-East-1 has most services

## Account Setup

Process:
- Create a Free Account
- Provide Credentials
- Provide Contact Info
- Verify Identity
- Choose Support Plan

### Exam Tips

- Just need to know the support plans
	- Basic, Developer, Business, Enterprise
	- Varying response times, prices, and levels of dedicated support/contacts
- Might be asked about Service Level Agreements e.g. response time

### Support Plans

- Basic
	- Account + Billing Support
	- No Technical Support
	- Access to Community Forums
	- Free
- Developer
	- For those experimenting with AWS
	- One primary contact to talk to - 12-24 hours response time
	- Starting at $29/month
- Business
	- For production use in AWS
	- 24/7 support by phone and chat
	- 1 hour response time in urgent cases
	- Help with common third-party software
	- Access to trusted advisor for optimisation
	- AWS Support API
	- Starting at $100/month
- Enterprise
	- For Fortune 500 companies
	- All features of business plan
	- TAM (Technical Account Manager)
	- Proactive Guidance and best practices
	- Support concierge
	- 15 minute response time
	- Starting at $15000/month

## Billing Alarms

Created in CloudWatch (Management & Governance) > Billing
Can use Static (a threshold) or Anomaly Detection mode
Create an SNS topic (simple notification service) and provide an email
Confirm subscription and then add alarm name and description

### Exam Tips

- Will be asked about 'automatic notifications' - just say to create CloudWatch alarm


## Let's Start to Cloud! Identity Access Management (IAM)

Can access IAM either:
- Programmatically (using access key ID and secret access key)
	- For example API, CLI
- With AWS Management Console (using password)
- With SDK (using access key ID and secret access key)

Security Status Checks:
- View on IAM Dashboard
- Delete Root Access Keys
- Activate MFA on Root Account
- Create Individual IAM Users
- Use Groups to Assign Permissions
- Apply an IAM Password Policy

**Root Account**

Simply the email you used to sign up
Best practice is not to use this account - use 'users' instead
Typically, setup MFA then lock MFA away

### Exam Tips

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

### Activating MFA

- Click 'Manage MFA'
- Security Credentials Page > MFA > Activate MFA
- Choose MFA Device Type
	- Virtual
	- U2F security key (e.g. Yubikey)
	- Other Hardware (e.g. Gemalto token)
- Complete setup - e.g. scan QR code

### Customise Signin Link

`https://alias.signin.aws.amazon.com/console`

(by default your account number will be in place of `alias`)

### Create IAM Users

- Alphanumeric characters only
- Decide access type
- Set permissions - either:
	- Add user to group
	- Copy permissions from existing user
	- Attach existing policies
- Can filter policies by job function
	- E.g. `AdministratorAccess` - full access
	- `PowerUserAccess` - full access to platform but no users & groups
- User inherits that group's attributes
- Can also add tags
- After creation, given access key ID and secret access key
	- Can email/download

Example admin policy (JSON format):

```json
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Effect": "Allow",
			"Action": "*",
			"Resource": "*"
		}
	]
}
```

Example power user policy:

```json
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Effect": "Allow",
			"NotAction": "iam:*",
			"Resource": "*"
		}
	]
}
```

See all managed policy JSONs here: [https://gist.github.com/bernadinm/6f68bfdd015b3f3e0a17b2f00c9ea3f8](https://gist.github.com/bernadinm/6f68bfdd015b3f3e0a17b2f00c9ea3f8)

### Apply IAM Password Policy

- Manage Password Policy
- Set various details:
	- Minimum length
	- Password reuse
	- Password expiry
	- Allow changing of passwords
	- Administrator reset required
- Click 'Apply Password Policy'

### IAM Credential Reports

Useful for auditing
- shows password policies
- shows enabled status, last use, last changed
- similar for access keys
- shows MFA status

Generate via IAM Dashboard > Credential Report > Download

### IAM Best Practices

- **Root Account**
	- Only use it to create AWS account
	- Don't use it to login
	- Give a user admin access if needed
- **Users**
	- One user should equal one human being
	- No phantom users
- **Users/Groups/Policies**
	- Always place users in groups
	- Apply policies to groups
	- Try not to apply to individual users
- **Password Policies**
	- Apply strong password policy
	- Apply rotation policy
- **MFA**
	- Enable MFA everywhere possible
- **Roles**
	- Use these to access services
- **Access Keys**
	- Use for programmatic access
- **IAM Credential Reports**
	- Use these to audit permissions

### Example from Lab

Creating developer access
- Create developers group
- Add users to group
- Give full access to group to:
	- DDB
	- Lambda
	- S3
	- API Gateway
- Policies to use:
	- `AWSDynamoDBFullAccess`
	- `AWSLambdaFullAccess`
	- etc...
- I created policy manually
	- Best practice to use AWS managed policies first

## S3 101

Oldest service
Secure, durable, highly-scalable object storage
Essentially somewhere to put flat files - i.e. something that doesn't change (a picture or video, not a database)

### Exam Tips

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
- Remember storage classes

### Basic Info

**Object-Based Storage**

Storing files, rather than storing something like an OS (block-based)

Data spread across multiple facilities

**Essentials**

- Object-based: file storage
- Unlimited storage
- Objects can be 0-5 TB
- Files stored in Buckets - essentially a folder in the cloud

### Buckets

Buckets have universal namespace - globally unique

Buckets have a unique URL:
`https://s3-region.amazonaws.com/bucketname`

Creates a DNS entry which is why it must be unique

**Uploading**

Always receive a HTTP `200` code if successful

### Object-Based Storage

- Key (name)
- Value (data)
	- Makes up contents of object
	- Series of bytes
- Also other data:
	- Version ID
	- Metadata
	- Subresources (Access Control Lists, Torrent)

### Data Consistency

Read-after write consistency for PUTS of New Objects
- if writing a new file (PUTting) and you read it immediately afterwards, that data will be readable

Eventual consistency for overwrite PUTS and DELETES (can take some time to propagate)
- if you update an existing file, or
- if you delete a file
- if you immediately read that file you may get the older version

Is there a way to tell if object has updated?

### S3 Guarantees

- Built for 99.99% availability (seconds in a month)
- Only guarantee 99.9%
- Guarantee 11 9s durability (99.999999999%)

### S3 Features

- Tiered Storage
- Lifecycle Management
- Versioning
- Encryption
- Securing Data
	- Access Control Lists (per file)
	- Bucket Policies (whole bucket)

#### Transfer Acceleration

Fast, easy and secure transfer of files over long distances between end users and an S3 bucket

Uses CloudFront's Edge Locations
- Users upload to an EL rather than directly to the bucket
- As data arrives at an EL it is routed to an S3 over an optimised network path

Uses Amazon's internal network (not the internet)

#### Cross Region Replication

Bucket is automatically replicated to another region
- primary bucket in region A
- file uploaded to primary bucket, also uploaded to secondary
- disaster recovery

### Storage Classes

Each storage class has different durability, availability, number of AZs, storage charges, retrieval fees, and first byte latencies.

![[Pasted image 20210421125501.png]]

**S3 Standard**
- 99.99% availability, 11 9s durability
- Stored redundantly across devices
- Built to sustain loss of 2 concurrent sites

**S3 - IA**
- Stands for 'infrequently accessed'
- Rapid access when needed
- Lower storage fee, charged per access

**S3 One Zone - IA**
- Same as above, but lower cost option
- Don't require multiple AZ resilience

**S3 - Intelligent Tiering**
- Optimises costs, powered by ML
- Analyses usage patterns
- Automatically moves data to most cost effective tier
- No performance impact/operational overhead

**S3 Glacier**
- Secure, durable, low cost class for data archiving
- Competitive price for on-prem solutions
- Retrieval times are configurable from minutes to hours

**S3 Glacier Deep Archive**
- Lowest-cost storage class
- Retrieval time of 12 hours

**S3 Outposts**
- Delivers object storage to on premise AWS Outpost environments

### S3 Charges

- Storage
	- per GiB
- No. of Requests
- Storage management pricing
- Data transfer pricing
- Transfer acceleration
- Cross region replication pricing

## Creating an S3 Bucket

### Exam Tips

- Names must be globally unique and DNS compliant
- Buckets are viewed globally but can be situated in individual regions (for latency)
- Can use CRR to replicate from one region to another
- Can change storage classes and encryption of objects on the fly
- Remember storage classes
- Restricting Bucket Access/Controlling permissions
	- Bucket policy applies to whole bucket
	- Object policies are per object
	- IAM policies can grant access to users and groups
- Allowing public access on bucket doesn't automatically make objects public - just means they *can* be public
- You cannot make an object public while public access is blocked

### Creation

Services > Storage > S3
Region changes to Global (like IAM)

Creating the bucket:
- name must be DNS compliant
- specify region to deploy into
- can copy bucket settings

Configure options
- can add versioning, server access logging
- decide public access settings
	- can block all public access
	- or can set granular options like ACLs, cross-account access

Click into bucket > press Upload or Create folder to upload objects

### Object and Bucket Properties

Files are not public by default (XML access denied error)
- use Actions > Make Public
- or Select Object > Permissions > Public access > Everyone

Bucket properties
- static website hosting
- object lock
- object tags
- transfer acceleration
- event notifications
- requester pays etc..

Permissions tab
- allows managing public access settings

Management
- lifecycle management e.g. send to glacier after 90 days
- replication - cross-region replication setup

File properties
- set encryption
- set storage class
- set transfer acceleration
	- can do a speed comparison from this screen

## Creating a Serverless Static Website on S3

### Exam Tips

- Can make entire buckets public with bucket policies
- Use S3 to host static sites (HTML, CSS, Javascript)
	- No dynamic sites (databases etc)
- S3 scales automatically to meet demand

### Uploading Objects

Storage > S3 > Create Bucket
Make whole bucket public access enabled and type *confirm*
Upload objects and make public
- can do this individually per file
- or can create a bucket policy to make all objects public

#### All Public Objects Bucket Policy

Permissions > Bucket policy > Edit

```json
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "PublicReadGetObject",
			"Effect": "Allow",
			"Principal": "*",
			"Action": [
				"s3:GetObject"
			],
			"Resource": [
				"arn:aws:s3:::BUCKET_NAME/*"
			]
		}
	]
}
```

### Configuring as Site

All hosted on S3 - no servers required

Then configure as a website:
- Properties > Static Website Hosting > Enable
- Set index path
- Set error path
- Save changes

This then provides a new domain name

## S3 Versioning

### Enabling Versioning

Properties > Versioning > Enable
- once enabled you cannot disable, you can only suspend

Click 'list versions' tab

Now uploading a new version of a file will replace that file
- null version is default
- newest version appears at the top

Can visit URLs for individual versions

Can rollback to previous versions
- Actions > Delete will rollback to original

### Exam Tips

- Stores all versions of an object
	- All writes
	- All deletes
- Great backup tool
- Versioning cannot be disabled once enabled - only suspended
- Integrates with lifecycle rules - e.g. archive old version
- Can use versioning with MFA delete - prevents deletion without MFA

## CloudFront

Amazon's Content Delivery Network (CDN)
System of distributed servers that delivers webpages and other web content to a user based on their geographical location, origin of the webpage, and a content delivery server

Latency can be high if connecting to a server directly

### Exam Tips

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

### How it works

Key pieces
- Edge Locations (ELs) - where cached content is stored
- Origin - origin of files CDN will distribute
	- Could be S3, EC2, ELB, R53
- Distribution (CDN) - collection of ELs

How it works (if CF turned on)
- Users query ELs & see if the content is cached
	- Does the user do this, or do they request content and then AWS queries EL?
- If not, they download it from the origin
- If so, download it from EL
- First user will always have latency but after that all other users can access it

File is cached for a specific TTL (time to live), in seconds
- default TTL is 24 hours

Can deliver all kinds of content
- website
	- dynamic, static and streaming content
	- interactive content
- requests automatically routed to nearest EL - best possible performance

### Distribution Types

- Web Distribution - typically used for websites
- RTMP - used for media streaming e.g. flash - uncommon now

### Setting up CloudFront

Networking & Content Delivery > CloudFront

Create Distribution
- Select Delivery method (Web or RTMP)
- Set origin domain name e.g.
	- S3
	- ELB
	- Media Package
	- Media Store Endpoint
	- HTTP server on EC2
	- Any other kind of host
- Set optional origin path e.g. subfolder in bucket
- Restrict bucket access - i.e. only via CloudFront, or also via S3
- Set HTTP/HTTPS only
- Set TTL

Creates a domain name for distribution
- `randomstring.cloudfront.net`
Commonly takes >30 minutes to setup

### Getting Content

`randomstring.cloudfront.net/filepath`


### Deleting Distribution

Select Distribution > Disable > Wait > Delete

## EC2 101

Elastic Compute Cloud
One of oldest services
Features regularly

Virtual server in cloud
Reduces time required to obtain and boot new server instances to minutes
Allows scaling capacity up and down very quickly as requirements change

Before AWS, contact a managed server provider like rackspace
Rack and stack, bring up to spec, sign contract
Deployment times from ~2 weeks to 6 months

Changed whole industry overnight

### Exam Tips

- EC2 is web service that provides resizable compute capacity in cloud - essentially a virtual server in the cloud
- Reduces time required to obtain and boot new server instances - allows quickly scaling up and down
- 4 pricing models: on-demand, reserved, spot, and dedicated hosts
- Not charged for spot instances for partial hour if automatically terminated
- EC2 Instance Types - **FIGHTDRMCPXZAU** - See [[Chapter 2 - Cloud Concepts & Technology#EC2 Family Mnemonic|Mnemonic]]
- EBS is virtual disk in cloud - types include GP2, IO1, ST1 and SC1

### Pricing Models

1) On Demand
	- Fixed rate by the hour/second
	- No commitment
2) Reserved
	- Capacity reservation
	- Significant discount on hourly charge
	- Locked in to contract - 1 or 3 year terms
	- More you pay up front, better discount
	- Most cost effective way to pay for EC2 is 3 years, all up front
	- Types:
		- Standard Reserved: Up to 75% off; cannot change between instance families (e.g. compute, memory optimised)
		- Convertible Reserved: Up to 54% off; can change attributes of RI as long as exchange results in creation of Reserved Instances of equal or greater value (professional level certs)
		- Scheduled Reserved: Available to launch within tie windows you reserve only; allows you to match capacity reservation to predictable recurring schedule
3) Spot
	- You bid whatever price you want for instance capacity
	- Instances are 'spare computing power' at a significant discount
	- Price moves around as people bid
	- If it hits your bid price it provisions it
	- If it goes above your price you lose the server
	- If spot instance is terminated by Amazon EC2 - price gone above what prepared to pay, won't be charged for partial hour of usage - but if you terminate instance yourself, you will be charged
	- Essentially "terminated in ascending order of bids"
	- Fine if you aren't worried about losing your server
	- **NEW MODEL FOR SPOT**
		- No longer uses bidding
		- Prices set by AWS, you pay the spot price that's in effect for the current hour
		- Request spot capacity just like requesting on-demand capacity
		- Source: [https://aws.amazon.com/blogs/compute/new-amazon-ec2-spot-pricing/](https://aws.amazon.com/blogs/compute/new-amazon-ec2-spot-pricing/)
4) Dedicated Hosts
	- Physical EC2 servers dedicated for your use
	- Can help reduce costs by using existing server-bound software licenses

**Use Cases**
- On demand:
	- Low-cost and flexibility of EC2 w/ no up-front payment or long-term commitment
	- Applications w/ short term, spiky, or unpredictable workloads that cannot be interrupted
	- Applications being developed or tested on EC2 for first time
- Reserved:
	- Steady state/predictable usage
	- Require reserved capacity
	- Users are able to make upfront payments to reduce costs
- Spot:
	- Applications with flexible start and end times
	- Applications that are only feasible at very low compute prices
	- For example engineering companies who do lots of computing at night - see [case studies](https://aws.amazon.com/ec2/spot/testimonials/)
	- Users with urgent computing needs for large amounts of additional capacity (but only if spot price is lower than on demand)
- Dedicated Hosts:
	- Regulatory requirements that may not support multi-tenant virtualisation (e.g. the law requires you be on dedicated host)
	- Licensing that does not support multi-tenancy or cloud deployments (e.g. Microsoft, Oracle, VMWare licensing)
	- Purchased on-demand (hourly) or by reservation (up to 70% off)

### EC2 Instance Types

Don't need to know these off by heart for associate/CCP
Useful for sysops admin, professional speciality

![AWS Certified Solutions Architect Summary – Jose Carvajal – Passionate  Software Engineer](https://sgitario.github.io/images/aws-ec2-instance-types.png)

Types:
- F class (Field Programmable Gate Array) - Reconfigure underlying hardware after chip manufactured
	- Use case: genomics, finanical analytics, big data etc
- I class - High speed storage
	- NoSQL, Data warehousing
- G class - Graphics Intensive
	- Video encoding, 3D app streaming
- H class - High disk throughput
	- Distributed filesystems etc
- T class - Lowest cost, general purpose
	- Web servers, small databases
- D class - Dense storage
	- File servers, warehousing, hadoop
- R class - Memory optimised (R for RAM)
- M class - General purpose
	- Application servers
- C Class - Compute optimised
	- CPU intensive apps and DBs
- P class - Graphics/General Purpose GPU
	- Machine learning, bitcoin mining
- X class - 'Extreme' memory optimised
	- SAP HANA, apache spark
- Z1 class - high compute and memory footprint
	- High per-core licensing costs
- A1 class - Arm-based workloads
	- Scale-out workloads
- U class - Bare metal
	- Bare metal capabilities that eliminate virtualisation overhead

Don't need to know this - comes in use later on
E.g. know that there's no such thing as a 'K' class - allows discounting answers

#### EC2 Family Mnemonic
- "Fight Dr McPixie in Australia"
- F - FPGA
- I - IOPS
- G - Graphics
- H - High Disk Throughput
- T - Cheap General Purpose (i.e. T2 Micro)
- D - Density
- R - RAM
- M - Main choice for general purpose apps
- C - Compute
- P - Graphics (pics)
- X - Extreme memory
- Z - Extreme memory and CPU
- A - Arm-based
- U - Bare metal

How intuitive..

### EBS

Virtual Hard Disk used by EC2
Every server has disk, every virtual server has virtual disk
Create storage volumes, attach to EC2
Once attached, can:
- create file system
- Run database
- Use in any way you would use a block device

EBS volumes in a specific AZ
Automatically replicated to protect from failure
In same AZ as EC2
Essentially a virtual disk in the cloud

**SSD**
- General Purpose SSD (GP2) - balances price and performance, wide variety of workloads
- Provisioned IOPS SSD (IO1) - maximised IOPS (input-output per second) - critical low-latency or high-throughput workloads

**Magnetic**
- Throughput Optimised HDD (ST1) - low-cost hard disk drive - frequently accessed, throughput-intensive
- Cold HDD (SC1) - Lowest cost HDD, designed for less frequently accessed workloads (file servers)
- Magnetic - previous generation

## Using EC2 Lab

### Exam Tips

- EC2 is compute based - it is not serverless, it's a server in the cloud!
- Connect to EC2 using private key
- Remember common ports: SSH, RDP, HTTP/S
- Security Group is essentially a virtual firewall
	- Let everything in: `0.0.0.0/0`
	- Let specific IP in: `a.b.c.d/32`
- Always design for failure - have one EC2 in each availability zone

### Deploying

Can filter by free-tier only
Multiple AMIs available (Amazon Machine Image)
- Essentially operating systems
- Some come with .NET core etc
- Amazon Linux 2 is recommended for many use cases

Instance type availability depends on region
- t2.micro is free

Configure details
- Number of instances
- Decide if Spot Instances to be used
- Pick network (VPC) and AZ
	- Subnet dropdown default choice is randomised so not everyone picks same one
- Can assign IAM role

Add storage
- Create an EBS
- Choose volume type (GP2, IO1, Magnetic Standard)
- Can only boot from above - adding a new disk can use SC1, ST1 also

Add tags
- key-value pairs

Configure Security Group
- Essentially virtual firewall in the cloud
- Computers talk on different ports - e.g. SSH traffic on 22, RDP on 3389, HTTP on 80, HTTPS on 443
- Let everything in on `0.0.0.0/0`, `::/0`
- Or let just one IP access - `a.b.c.d/32`
- Can configure to accept "my IP"

Launch instance
- Lets you create new/use existing SSH key
- Store this securely - one copy of private key
- One launched, supplies public/private IP address to connect

## Launching EC2 Instance in Custom Virtual Private Cloud

Lab - covers following objectives:
- create custom VPC
- create public and private subnets
- create routes and configure internet gateway
- launch EC2 instances in subnet
- access EC2 instances

## Using the AWS Command Line

### Exam Tips

3 ways to interact:
- Console
- CLI
- SDKs (beyond this course - uses programming language libraries)

### Using Secret Access Key

User security credentials
- given programmatic access - uses access key
- to generate a new one, press make inactive, delete key, and create key again

Click EC2 > click connect > use EC2 instance connect
- can also use Putty/SSH
- Login with `ssh -i /path/to/pem ec2-user@[IP]`
- Type `sudo su` to elevate to root

Command line basic usage:
- `aws [service] [command] [options]`
- E.g. `aws s3 mb s3://bucket-name`
- `aws [service] help` to see commands

First, need to add credentials:
- Either give creds for account using `aws configure`
	- Input access key ID, secret access key, default region and output format
	- Exposing the secret key gives away full access to that user!
- Or use roles

Example commands:
- `aws s3 ls` - lists buckets
- `aws s3 cp /path/to/file s3://path/to/bucket` - copies local file to bucket

Credentials stored in `.aws/credentials`
- this means that a compromised server exposes creds
- Try not to use secret access key where possible
- Use roles instead

## Using Roles

### Exam Tips

- Roles are more secure than storing access keys on an EC2
- Easier to manage
	- Adding more policies to role updates instantly
- Can apply to instances at any time - change takes place immediately

### Creating Role

Remove old access key first

Services > IAM > Roles > Create role
- attach/create permission policies
	- e.g. `AmazonS3FullAccess`
- tag role
- name role and set description
	- e.g. "allow EC2 to use S3 as admin"


### Attach Role

- Tick EC2
- Press Actions > instance Settings > Attach Replace IAM Role
- Choose Role > Apply

Can then clear the credentials from EC2 to stop it using creds
- `rm -rf .aws`

Then execute commands
- it now uses the role attached
- no creds are stored on the EC2
- if the EC2 is hacked, we can simply delete it and create a new EC2 - the hacker will lose access

## Using EC2 as a Webserver

SSH in and update
- `sudo yum update -y`

Install apache
- `sudo yum install httpd -y`

Start httpd (apache)
- `service httpd start`

Add files in `/var/www/html`

Won't be tested on this - but need to learn how load balancers work

## Let's Use a Load Balancer

### Exam Tips

3 types:
- application - layer 7 aware, intelligent decisions
- network - extreme performance, static IPs
- classic - test & develop, keep costs low

Keep EC2s in multiple AZs to have little to no outage

Allows fault-tolerant architecture

### Creating

Services > EC2> Load Balancer > Create Load Balancer

3 types:
- Application load balancers - application aware (layer 7) - intelligent routing decisions
- Network Load Balancers - ultra high performance, static IPs
- Classic Load Balancers - slowly getting phased out

Internet-facing for web server

HTTP listener on port 80

Select VPC
- then select availability zones
- can put instances in any of these AZs

Configure HTTP/S

Select Security Group

Configure Routing:
- set target group (can create new one)
	- name
	- target type (instance, IP, lambda)
	- protocol
	- port
- health checks
	- protocol and path
	- port
	- healthy threshold (how many responses it needs) and interval (how often polled)

Register targets
- add instances to registered list

Then review + launch - can take 5-10 minutes to setup (provisioning)

### Creating New Webserver

New Instance - then choose an AZ that you don't have an EC2 in yet

Advanced Details:
- add a bootstrap script to run httpd as EC2 boots
- means you don't have to login to install apache and apply updates

Example:

```
#!/bin/bash
yum update -y
yum install httpd -y
service httpd start
chkconfig on
cd /var/www/html
echo "<html><body><h1>WebServer 2</h2><body><html>" > index.html
```

Once launched, you won't need to login - can visit webserver directly at IP

Can you replicate an EC2?

### Testing LB

Go to DNS name - DNS name now resolves to EC2 instances, don't have to use public IP addresses

Add new EC2 behind load balancer:
- load balancing
- target groups
- edit
- add new instance to registered
- save
- wait

Gives status as initial
Once it becomes heathy, can be browsed to
Refreshing might return a different page
If terminate an instance, no downtime - just redirects to other server

## Databases 101

### Exam Tips

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

### Relational Databases

Think of a traditional spreadsheet - xslx file is the database, has a number of tables each with rows and columns
Databases are similar
Adding a column affects all rows

Amazon's relational database service is RDS
Many flavours (database engines):
- Microsoft SQL Server
- Oracle
- MySQL Server (open source)
- PostgreSQL (open source)
- Aurora (AWS proprietary)
- MariaDB (open source)

RDS Key Features:
- multi-AZ for disaster recovery
	- Lose one, RDS automatically fails over
- Read replicas - for performance
	- Copies of database
	- Instances read from read-replicas rather than production DB - frees up DB performance

AWS point connection string to primary DB usually
If it goes down, AWS automatically detects it and fails over to secondary DB

For read replicas, writes go to primary DB first and are replicated to read replicas
If main one dies, there's no failover to read replica - instance will go down as there will be no write ability
But can be setup so all writes go to primary, reads go to replicas
Up to 5 copies of database in read replicas
Better performance - spreads the load

### Non Relational Databases

More recent tech

Consist of collection (table)
Inside this - document (row of data)
Document consists of key-value pairs (fields)

So what's the difference?

Key value pairs:

```json
{
"_id":"UID",
"firstname":"John",
"surname":"Smith",
"address":[
{"street":"Street Name",
"suburb":"Suburb Name"}
]
}
```

Can be either nested or flat
As many nested columns as you like
Columns can vary, won't affect other fields (rows)
I.e. one entry can have many fields, next entry may only have a few
Extremely flexible

AWS' is called DynamoDB


### Processing

**Online Transaction Processing (OLTP)**

Pretty simple - standard queries such as "show me order 21021" - retrieves all data from the database row, or inserts data - etc.

**Online Analytics Processing (OLAP)**

More complicated
May be a management team wishing to calculate figures such as net profit
Will be retrieving a huge number of records + perform calculations
This has a large performance cost

This is where **data warehousing** comes in
So can do OLAP away from prod database
Complex queries not impacting primary DB - affects database custom built for this
Business Intelligence - tools include Cognos, Jaspersoft
Used for large and complex datasets

They use different architecture both from DB and infrastructure perspective - built from ground up for this purpose
AWS' product is **RedShift**

### ElastiCache

Web service that makes it easy to deploy, operate and scale an in-memory caching service in the cloud
Improves performance of web apps by allowing to retrieve info from fast, managed, in-memory caches instead of relying entirely on slower disk-based databases

Essentially allows quick retrieval of common items
- if same info comes up often, no need to query hundreds of thousands of times
- Elasticache caches most common queries and returns them much faster
- Takes huge load of prod database

Two open-source caching engines supported:
- Memcached
- Redis

## Let's Provision an RDS Instance (+ WordPress)

Steps:
- Provision RDS Instance
- Open Up MySQL Port to Webserver Security Group
- Create an EC2 instance to host Webserver on
- Install Wordpress using bootstrap script (user data)
- Register EC2 instance to target group & create Application Load Balancer - DNS name will map back to EC2s
- Update Wordpress to use DNS name of ALB
- Take a snapshot of EC2

Not tested on this in exam

### Provision RDS

RDS > Create Database > Select Engine

Aurora keeps six copies spread across AZs
Overkill for our use case - choose MySQL
Choose a template
- production is high availablity, consistent and fast performance
- dev/test is intended for dev use
- free tier is for quickly testing and developing

Settings:
- instance identifier (essentially title)
- username + master password
- instance size (standard class is very large and expensive by default)
- storage: provisioned IOPS way more expensive than general purpose SSD
- autoscaling can be left on
- Multi-AZ deployment - standby instance
- select VPC
- additional config - name DB (creates initial database, but can do so manually in CLI later)

Estimates monthly cost

Then can take 10-15 mins to provision

Monitoring shows CloudWatch metrics

Connectivity & Security Tab gives DB endpoint address
- wordpress can connect to this address

### Wordpress VPC Settings

Add rule for MySQL traffic - preset setting for MySQL/Aurora (3306)
Set source to security group `sg-securitygroupname`

### Wordpress EC2

Launch instance > Amazon Linux > Advanced Details > User Data:

```bash
#!/bin/bash
yum install httpd php php-mysql -y
cd /var/www/html
wget https://wordpress.org/wordpress-5.1.1.tar.gz
tar -xzf wordpress-5.1.1.tar.gz
cp -r wordpress/* /var/www/html
rm -rf wordpress
rm -rf wordpress-5.1.1.tar.gz
chmod -R 755 wp-content
chown -R apache:apache wp-content
service httpd start
chkconfig httpd on
```

Leave rest of settings as they are.

Select existing security group, add to `sg-securitygroupname` (the group that is approved to communicate with RDS)

### WordPress

Can now visit wordpress at public IP address
- hit `Let's go`
- configure database details (uname, password, dbname)
- database host is endpoint string
- submit details
- create `/var/www/html/wp-config.php` on EC2 with details provided
- hit `run the installation`
	- Site title
	- username
	- password
	- email
- Login and change settings
	- change wordpress address from EC2 public IP (not static) to DNS address (this is where load balancer comes in) - you could also use a R53 DNS name etc

### Wordpress ALB

- Create an ALB
- Create web servers target group
- Add EC2 to registered targets
- Take ALB DNS name and save it to Wordpress Address
- These details go to RDS (wordpress config database)
- If EC2 goes down, it's fine - just spin up a new one and add it to target group

**Create Image**

Can use this when doing autoscaling groups
Means don't have to reinstall wordpress each time

Steps:
- Instance > Actions > Image
- Set image name
- Hit Create

Takes some time but then can be used to spread across multiple AZs - right now RDS is split, but EC2 only in one

## Autoscaling

Currently our setup has a single point of failure, the EC2:

![[Pasted image 20210511082409.png]]

(*source:* [https://medium.com/awesome-cloud/aws-difference-between-multi-az-and-read-replicas-in-amazon-rds-60fe848ef53a](https://medium.com/awesome-cloud/aws-difference-between-multi-az-and-read-replicas-in-amazon-rds-60fe848ef53a))

In the diagram above there is a Route 53 setup, but that can be interchanged with a Load Balancer in our case.

For redundancy, we can use our AMI (image) of our EC2 to deploy a second EC2 in a separate Availability Zone using autoscaling, for a fault tolerant website.

### Demo

- EC2 > Terminate Current Instance (we have a snapshot)
- Scroll down to Autoscaling
	- Launch Configuration > Create a launch configuration > My AMIs > Select
		- Select EC2 size
		- Add more User Data (for some reason this not included in image - maybe it is for all machines in group) - `yum update -y`
		- Name the configuration
		- Add storage and security groups
		- Create launch configuration > select private key
	- Create Auto Scaling Group (button to do this with current LCG)
		- Name Group
		- Select LC
		- Select size (no. instances)
		- Select network and subnet (list of subnets to choose from - will spread across subnets automatically - subnets equivalent to AZs - if launched in one, will launch next in another)
		- Advanced Details > Target Groups > LoadBalancer Group
		- Set Health Check type to `ELB`
		- Set Service-Linked Role (can click to view role in IAM - 	`AutoScalingServiceRolePolicy` by default)
		- Configure Scaling Policies > Adjust capacity of this group or Keep at initial size > scale between X and Y instances > Metric type > Average CPU Utilization (target value in %)
		- Can then set notifications and tags

Can view auto scaling groups
- gives activity history
- can see running instances in EC2 - each have a subnet from list
- then can visit via ALB DNS as usual
- now we have a fault tolerant website - EC2s in different AZs, ALB running to balance, autoscaling to 

To teardown, delete Auto Scaling Group first, then EC2s then RDS, then ALBs (delete load balancer, then delete target group)

## Buying a Domain Name

### Exam Tips

Route53 is Amazon's DNS service
It is global, similar to IAM and S3 - no region specified
You can use it to direct traffic around world, and register domain names

### What is DNS?

Domain Name System
Like a phonebook - computers use it to resolve domain names to IP addresses
Looks them up, resolves an IP address, connects via IP address

Types of DNS records e.g. CNAME not relevant for DNS, but necessary for Solutions Architect

DNS is port 53, Route 53 named after this

### Setting up R53

Networking & Content Delivery > Route 53

High level for now - just covering registering a domain name

- Choose a domain name
- Make sure bucket is available with same name
- Create bucket with same name (full FQDN) - e.g. bucket name `domain-name.com`
- Enable static website hosting + allow public access + confirm
- Add bucket policy to make all objects public (see [[#All Public Objects Bucket Policy]]) + update ARN
- Back to R53 - add domain to cart, fill in registrant contact info (may take up to 3 days)
- Once email comes through, domain will show up on Dashboard and in Hosted Zones (list of domains you own)

Configure DNS:
- create record set
	- don't need to understand record types
	- register type A
	- Alias Record = Yes - naked domain name, no `www` - select target -> S3 website endpoints (S3 bucket must have *exact* same name, including `.com`)
	- now browsing to that domain serves up alias for S3 bucket DNS record, and goes to static site

## Elastic Beanstalk

Previously we had to configure our EC2s' apache etc with bootstrap script (user data)

Elastic beanstalk lets us provision EC2s, SGs, ALBs all with one click
Essentially a way of quickly deploying if you're unfamiliar with EC2

### Exam Tips

Can quickly deploy and manage apps in cloud, without worrying about infrastructure that runs applications
- don't need to worry about provisioning EC2, installing PHP etc
- just upload application code, and EB handles the rest
- decides details of capacity provisioning, load balancing, scaling, and application health monitoring

### Deploying

Elastic Beanstalk is under Compute
**POPULAR EXAM QUESTION** - select all compute services - remember EB is one!

Steps:
- Create a web app
- Application name
- Platform (e.g. PHP)
- Application code - sample app, or upload code

Creates:
- an environment
- a security group
- an S3 bucket to store environment data
- EC2 instance

Can view environment by clicking URL
Gives info about version name

Configuration:
- modify instance types
- add a load balancer
- change capacity from single -> multi-AZ

Big focus on EB in sys ops and dev ops exams

CCP is high level - just need to know what it is
- way of deploying apps to cloud
- don't need to know anything about AWS
- upload code, AWS inspects it and deploys automatically

Actions > Delete application to delete and unprovision all instances

## Cloudformation

One of AWS most powerful tools
Got Ryan interested - used to be an infrastructure architect
Multiple sites
MPLS circuits, failovers etc
Used to take 3-6 months - sheer scale

CloudFormation came along - turns infrastructure into code
Code can be deployed in multiple regions
Codify entire deployment, provision in minutes

"Knew they weren't playing around - became obsessed - knew as infra architect my days would be numbered"

### Exam Tips

Helps you model and set up AWS resources
- spend less time managing those resources
- more time focusing on apps that run within AWS

Create a template that describes all desired resources - EC2s, RDS, Lambda, VPCs, Subnets
CloudFormation takes care of provisioning and configuring resources
Handles all dependencies

EB and CF are both free - but the resources they provision *are not*
EB is limited in what it can provision and is not programmable - CF can provision almost any service and is fully programmable

### Creating a Stack

Management & Governance > CloudFormation

Can either:
- create a template in designer
- use a sample template
- or upload a template to S3

WordPress template:
- Set several params:
	- DBName, DBPassword, DBRootPassword, DBUser
	- instance type
	- key
- Add tags
- Create stack
- Wordpress template is EC2 and RDS

Outputs:
- gives a URL that can be used to access

Can take 5 minutes to several hours depending on stack complexity

CloudFormation deep dive course available
Essential for solutions architect exam and careers

### Capabilities

Can automate all sorts:
- provision instances of EC2, RDS, Lambdas
- setup networks
- install software

### Designer

Visual view of template

### Cleaning Up

Cloudformation > Stacks > Delete

### Alexa Skills Kit

Can use CloudFormation to provision Lambda Functions (Compute > Lambda)

Browse Serverless App Repository in Lambda

Designing Alexa Skills covered in Solutions Architect, Developer Associate courses

CloudFormation can deploy skills - don't need to know how to program

## Architecting for the Cloud - Best Practices

Based on [[AWS CCP Index#Read Whitepapers|AWS Overview Whitepaper]] - gives best chance of passing

### Exam Tips

Read the whitepaper the day before the exam

### Traditional vs Cloud Computing

**IT Assets as Provisioned (or *programmable*) Resources**
- 'Provisioned' from Oct 2018
- IT assets available as a programmable/provisioned resource
- E.g. cloudformation - take a JSON/YAML template and turn into instances within AWS Ecosystem
- Traditionally, you get a purchase order and purchase physical servers, enter a contract - rack and stack, install operating systems

**Global, Available, Scaleable**
- Cloud is faster to deploy
- it's also global, available, and has scaleable capacity

**Higher Level Managed Services**
- e.g. Machine Learning with Sagemaker - don't need an ML expert, use AWS services as a product

**Built-in Security**
- extremely secure, safer on AWS than to host yourself
- Given products such as web-app firewalls, IAM for groups and users to delegate levels of access, MFA setup etc

**Architecting for Cost**
- can design cloud environment to be super cost-efficient
- for example, A Cloud Guru building a serverless website for $400/month servers hundreds of thousands of users

**Operations on AWS**
- migrating to cloud - lift and shift VMs to EC2
- Re-factoring - take MySQL from VM and use RDS instead
- Re-architecting - move to serverless and make it cost-efficient

### Design Principles

#### Scalability

**Scale Up**
- e.g. take a t2.micro and increase size
- increase amount of RAM/CPU power

**Scale Out**
- more common
- e.g. adding multiple EC2s behind load balancer
- Many ways to do this:
	- Stateless applications e.g. Lambda
		- Alexa uses this - it doesn't remember what you've said, it just runs an algorithm in lambda and returns result
	- Distribute load to multiple nodes
		- for example, multiple EC2 servers, or RDS read replicas
	- Stateless components
		- More stateless your components, the easier application scales
		- For example, logging into web app - instead of storing sessions on server, store it in a cookie on user browser
	- Stateful components
		- Might keep cookie in browser, but also want to understand what user is doing
		- Instead of storing in browser and losing it, you want to store that info in a DB
	- Implement Session Affinity
		- E.g. cookie in browser for sticky sessions - LB detects this and forwards to a specific EC2 - 'stuck' to that instance
	- Implement Distributed Processing
		- For example, Elastic Map Reduce - different EC2s processing complex jobs, reducing compute time

#### Disposable Resources Instead of Fixed Servers

We want stuff like EC2, rather than a fixed physical server - more flexible

**Instantiating Compute Resources**
- For example, bootstrapping
	- not configuring resources every single time
- Golden images
	- used in autoscaling for example
	- image once setup and configured, then reuse it
- Containers
	- E.g. Docker
	- Beyond CCP scope
- Hybrid
	- Combination of containers and EC2s

**Infrastructure as Code**
- For example, CloudFormation

#### Automation

**Serverless Management and Deployment**

Ideally, serverless - no worrying about infra with Lambda and S3, they manage themselves - only need to worry about deployment, using things like code pipeline (for developer associate course)

**Infrastructure Management and Deployment**

For example
- AWS Elastic Beanstalk
- Amazon EC2 Auto Recovery
- AWS Systems Manager
- Auto Scaling

**Alarms and Events**

For example:
- Amazon CloudWatch alarms (e.g. billing)
- Amazon CloudWatch events
	- for example, triggering a lambda when a file uploaded to a bucket
	- proactively responding to change in environment
- AWS Lambda scheduled events
- AWS WAF Security Automations
	- WAF = Web application Firewall
	- Responds to people trying to exploit site - for example, detecting SQLi attempts

#### Loose Coupling

**Well Defined Interfaces**
- e.g. Amazon API Gateway for building APIs

**Service Discovery**
- if using a fixed IP to connect to a DB and the server fails, it will break the app
- if you connect to an RDS via DNS and you have multi-AZ, you'll have automatic failover - one component 'discovers' the other

Loose coupling essentially about making it difficult for things to fail
For example SQS (queue service) - EC2s poll queue - if one fails, another picks up - gives resilience

**Distributed Systems Best Practices**
- Graceful Failure in Practice
	- Don't just crash, tell the user what appens


#### Services Not Servers

- Use Managed Services - e.g. Lambda, S3, R53 - not relying on a physical server
- Serverless Architectures - no point of failure, no managing servers

For example:
- angular JS app running in browser on connecting devices
- API Gateway for queries - this pipes to custom functions in AWS Lambda behind the gateway
- other microservices for stuff like search (CloudSearch), authentication (Auth0), S3 for file upload/download, Firebase/Dynamo for streaming etc
- no servers - no EC2 instances - entire compute bill is $400/month

"No server is easier to manage than no server"
There are no sysadmins - nothing easier than that - just developers


#### Databases

**Relational Databases**
- Aurora
	- built from ground up
	- MySQL and PostgreSQL
	- Scalable
	- Available: 6 copies across >= 3 AZs
	- Anti-patterns - no need for joins or complex transactions - use No-SQL

**Non-relational Databases**
- Dynamo
	- Push-button scalability, now has auto-scaling also
	- High availability - multi-AZ
	- Anti-patterns - joins or complex transactions, use Aurora - also large binaries, use S3

**Data Warehouse**
- Redshift
	- Scalable
	- Available
	- Anti-patterns: not meant for OLTP


*Note:* Aurora and DDB anti-patterns seem to be the same, but couldn't find any clarification in the whitepaper

**Search**
- CloudSearch and ElasticSearch
	- Don't come up often
- Scalability
- Available (always >= 2 AZs)

**Graph Databases**
- Amazon Neptune fully managed Graph DB
- Scalable
- Available

#### Managing Increasing Volumes of Data
- Data Lake
	- Architectural approach for massive amounts of data in central location
	- Ready to be categorised, processed, analysed and consumed by diverse groups
	- Can be stored as is - no predefined schema
	- Ideal place for data lake is S3 - can use Athena to run SQL on it

#### Removing Single Points of Failure

- Always introduce redundancy
- Mechanisms to Detect Failure
- Durable Data Storage - don't have important stuff on S3 with one-zone storage class, have it on normal S3
- Multi-data centre resilience - auto failover if AZ goes down - region-based failover good too
- Fauilt Isolation - how to isolate a fault if it occurs
- Traditional Horizontal Scaling - Scale out
- EMR Data Sharding - split across multiple shards, can process faster

#### Optimize for Cost

- Right size (e.g. EC2)
- Elasticity (small @ low demand, expand, shrink back)
- Take advantage of variety of purchasing options
	- Reserved capacity
	- Spot instances


#### Caching

- Application Caching e.g. Elasticache
- Edge Caching e.g. CloudFront and other CDNs


#### Security

- Use AWS Features for Defence in Depth (e.g. WAFs)
- Share security responsibility with AWS - See [Shared responsibility model](https://aws.amazon.com/compliance/shared-responsibility-model/)
- Reduce Privileged Access - give users least privilege - enough to do their job
- Security as Code - golden environment with hardened EC2 instances (patches etc), reference these with CloudFormation and deploy around the world
- Real-time auditing e.g. AWS Inspector, CloudTrail

**Shared Responsibility Model**

![[Pasted image 20210513083546.png]]

## Global AWS Services

Identify which are global and which are regional

### Global Services

- IAM
	- users are global
- Route 53
	- domains are global
- CloudFront
	- CDNs are global
- SNS
- SES

###  Regional Services With Global Views

- S3
	- view all in one panel
	- but each bucket is in a region

## Services that can be Used On Premise

Use in your own datacentres/corporate headquarters

### On-prem Services

- Snowball
	- Essentially gigantic disk - load all data on it, send back to Amazon
	- Usually 80 TB
	- If you have a huge amount of data and a 100 Mbps line, takes a long time to upload to AWS
	- Snowball lets you load data and then AWS upload it to S3 within a few days
- Snowball Edge
	- Also has a CPU
	- Allows deploying Lambda on premise
	- Boeing use it to test aircraft
	- I.e. need AWS resources but can't get AWS connectivity
- Storage Gateway
	- Similar to snowball, stays on-prem always
	- Can be physical or virtual (VM)
	- Essentially way of caching datacentre files
	- Replicates files to S3
	- If internet connection lost, still have them locally
- CodeDeploy
	- Way of deploying code to EC2 instances, but can also use it to deploy code to on-prem webservers
	- Just need to know what it does - deploys apps to servers
- Opsworks
	- Similar to Beanstalk, but more focused on devops
	- Uses Chef to do automated deployments
	- Deploy to EC2, or to on-prem webservers
- IoT Greengrass
	- IoT but connects devices to cloud

### For Deploying on Prem

These can be used to deploy code on prem:
- CodeDeploy
- Opsworks

## CloudWatch 101

### Exam Tips

- Used for monitoring performance
- Can monitor most of AWS
- Can also monitor apps running on AWS
- Can setup custom metrics e.g. number of visitors on site, number of active database connections
- CloudWatch EC2 monitors every 5 minutes by default - 1 minute intervals by turning on detailed monitoring
- Can create CloudWatch alarms that trigger notifications
- CloudWatch all about performance

### What is CloudWatch?

Monitoring service to monitor AWS resources, as well as applications runnnig on AWS

All about monitoring performance - like PT at gym
In AWS terms, can monitor:
- Compute
	- EC2 instances
	- Autoscaling Groups
	- ELB
	- R53 Health Checks
- Storage & Content Delivery
	- EBS Volumes
	- Storage Gateways
	- CloudFront

### Host Level Metrics

Underlying physical host - Ec2 always sitting on a physical server somewhere - CloudWatch can monitor this:
- CPU
- Network
- Disk
- Status check (health)

## AWS Systems Manager

Allows managing EC2 instances at scale
Multiple EC2 instances is called a fleet

### Exam Tips

Just high-level
- can be used to manage fleets of EC2 instances and VMs

- Piece of software installed on each VM
- Can be both inside AWS and on-premise
- Run Command used to install, patch, uninstall software
- Integrates with CloudWatch to give dashboard of entire estate

### What is it?

SSHing into all and running a simple command will take a long amount of time

Systems Manager
- when you setup an EC2, install a small piece of software
- this connects EC2 to Systems Manager
- can use Systems Manager to perform a Run Command
- can do this to run across all instances at once
	- can use it for updating via `yum update`
	- can use it for patching

Management & Governance > Systems Manager
- installing beyond scope - sysops administrator
- can use Run Command
- can use Patch Manager
- can setup Maintenance Windows

Can deploy this software on on-premise servers also
Manage your on-prem inside AWS

## Service Health Dashboard

### Exam Tips

- Just need to know that this is the method used if asked about how you can view an outage based on service
- Also like to confuse you with personal health dashboard

### What is it?

Exactly what it sounds like - view health of each AWS Service
Overview of regions - all regions, health of each service in region
Can view historical info on per-day basis
Gives you RSS feeds - can subscribe and get notifications e.g. if a service goes down

Can search 'AWS Service Health Dashboard' to view, or go to `https://status.aws.amazon.com`

## Personal Health Dashboard

### Exam Tips

Remember difference:
- service health dashboard shows all services
- personal health dashboard just shows services you use

### What is it?

- Personalised for you
- Service Health shows every service in every region - won't necessarily need this
- PHD shows overview of services you actually use, and what their status is
	- any availability issues
	- up to date info on service status
	- proactive notifications on scheduled activities

Management & Governance > Personal Health Dashboard

Can create rules to set up alerts

## S3 vs EBS vs EFS

### Exam Tips

Scenario-based questions on exam - test you on which storage medium you should use

Storing objects/files -> think S3
Storing OS/DB -> think EBS

- S3: flat files - pictures, docs, videos - not operating systems, databases
- EBS: virtual disk attached to EC2 - can store non-flat files - size can change, but not automatically - can attach to multiple instances now, but once couldn't
- EFS: virtual disk attached to EC2 - can be attached to multiple instances - size is elastic, scales up and down

### What is S3?

Provides developers and IT teams with secure, durable, highly scalable object storage
Easy to use, with web services interface
Great place to store objects (files)
You can't install an operating system on S3, or upload a database - used for flat, static files that don't change
Data spread across multiple devices/facilities

### What is EBS?

Stands for Elastic Block Store - storage volumes
Virtual hard disk in cloud
Persistent block storage volumes for use with EC2
Perfect for installing operating systems, uploading databases
Can also store files on EBS, but not same levels of redundancy, and harder to make objects publicly accessible

Automatically replicated, but only within its availability zone - protects from component failure
Availability, but within one AZ

### What is EFS?

Elastic File System - file storage service for EC2 instances
Similar to EBS - for storing databases etc
But not a set size - EFS automatically resizes itself to fit data
Good for content management systems, file servers
Multiple EC2s can access same EFS file store
Central management systems will probably use EFS
Create and configure file systems easily

EBS vs EFS key difference: EFS resizes as you add and remove files (elastic)

## Global Accelerator

### Exam Tips

Know what it is and where you'd use it
- create accelerators to improve performance
- for global apps

Routes via AWS backbone, not the internet
Up to 60% performance increase

Scenario-based questions about increasing reliability/consistency when internet congested -> think Global Accelerator

### What is it?

High level
Create accelerators to improve availablity and performance of apps for local and global users
Essentially accelerating traffic
Direct traffic to optimal endpoints on AWS global network
Improves availability and performance for internet applications used by a global audience

### How it Works

Uses Amazon's dedicated network - like CloudFront
Sends traffic thru global infrastructure
Improves performance by up to 60%
It's not traversing internet via multiple ISPs - uses backbone network
If internet is congested, GA's automatic routing optimisations keeps packet loss, jitter, latency consistently low

## Summary

### Six Advantages of Cloud

- Capital Expense for Variable Expense (pay by the minute or second)
- Benefit from massive economies of scale (AWS have huge ability)
- Stop guessing about capacity (autoscaling to scale in line with demand)
- Increase speed and agility (fast deployment)
- Stop spending money running and maintaining datacentres (don't compete with Amazon)
- Go global in minutes

### Three Types of Cloud Computing

- Infrastructure as a Service
- Platform as a Service
- Software as a Service

### Three Types of Deployment

- Public
- Private
- Hybrid

### Regions, Availability Zones, and Edge Locations

- Region is physical location in world, two or more AZs
- Availability Zone (AZ) is one or more discrete datacentres with redundant power etc
- Edge Locations are AWS endpoints used for caching content

### Choosing the Right Region

- Data sovereignty laws - regulation based on country etc
- Consider latency to end users - where are majority of customers?
- Consider availability of AWS services - not all available in all regions

### Understand Different Support Packages

- Basic: Free
- Developer: $29/month (scales on usage)
- Business: $100/month (scales on usage)
- Enterprise: $15,000/month (scales on usage) - get a TAM

|Level|Price ($/month)|Support|Response Time|
|---|---|---|---|
|Basic|Free|No technical support - community forums only|N/A|
|Developer|29|One primary contact|12-24 hours|
|Business|100|24/7 phone + chat, support API, trusted advisor|1 hour urgent|
|Enterprise|15000|Technical Account Manager, support concierge, proactive guidance|15 minutes|

### Billing Alerts & Alarms

- Automatic alerts when spending is reached

### Identity Access Management (IAM)

- IAM is Global - users and groups created globally
- Root account is email address used to signup - always full admin access, should not be given out/used - secure with MFA
- Group is a place to store users - users automatically inherit permissions of group - group permissions applied via policies, which are written in JSON and attached to group

### Access to AWS

- Console (web)
- Programmatically (command line)
- Software Development Kit (SDK)

### S3

- Object-based - store and upload files - between 0 and 5 TB
- Unlimited storage in buckets - folder in cloud
- Universal namespace - unique globally - each has a corresponding DNS name (`https://s3-region.amazonaws.com/bucket-name`)
- Only suitable for flat files - not operating systems and databases
- Uploading generates HTTP 200 status code if successful
- Key-value pairs: name and data
- Read after write consistency for PUTS of new Objects
- Eventual consistency for overwrite PUTS and DELETES (takes time to propagate)
- Buckets viewed globally but can be in different regions
- Cross region replication can replicate contents to another backup bucket in a different region
- Transfer acceleration allows users around world to upload to an Edge Location rather than a bucket, and transferred to S3 via Amazon backbone network
- Six types of S3 storage class:
	- Standard - 99.99% availability, multi-AZ, designed to sustain loss of 2 facilities concurrently
	- IA - infrequently accessed, but rapid access - cheaper, but charged retrieval fee - can also have one availablity zone
	- Intelligent tiering - machine learning to optimise storage class
	- Glacier - low cost, durable for archiving - minutes to hours retrieval time
	- Deep Archive - cheapest class, 12 hours retrieval time
- Bucket policies can make all objects public
- S3 can host a static website
- S3 scales automatically to meet demand - can put a static website on S3 if expecting a large number of requests

### CloudFront

- Edge locations all around the world - first time a file is requested, user checks against EL - if not, it downloads it, and subsequent requests taken from EL
- Caching speeds up subsequent requests
- Origin is the origin of files that CDN distributes - S3, EC2, ELB or R53
- Distribution is collcetion of ELs
- Web distribution used for sites, RTMP used for media streaming (deprecated)
- ELs are not just read only - can write objects, this is used for transfer acceleration
- Cached only for Time to Live
- Can clear cached objects, but will be charged

### EC2

- Web srevice providing resizable compute capacity in cloud
- Can scale up and down as computing requirements change
- Payment:
	- On demand (fixed rate by second)
	- Reserved (pay up front and reserve capacity, significant discount)
	- Spot (bid for spare capacity, but can lose instances if become more expensive - not charge for partial usage if cancelled, but are charged if you terminate yourself)
	- Dedicated hosts (useful for server-bound licenses etc)
- Instance types:
	- Several instance types for different purposes
	- FIGHTDRMCPXZAU
	- Don't need to know it off by heart for exam - but need to know which don't exist
- EBS
	- SSD or magnetic storage
	- GP2 - general purpose
	- IO1 - Provisioned IOPS
	- ST1 - Throughput optimised HDD
	- SC1 - less frequentily accessed workloads
	- Magnetic being phased out
- EC2 is a server, **not serverless**!
- Private key to connect to EC2 - SSH/RDP to connect

### Security Groups

- Firewalls used to decide which traffic to let in - security groups are virtual firewalls in the cloud
- Open up common ports

### Designing for Failure

- Things fail all the time - design with EC2s in more than one AZ

### Interacting with AWS

- Console
- CLI
- SDK

### Roles

- Use roles on EC2 to provide access, rather than storing access credentials on box
- Apply roles to EC2 instances at any time
- Roles are universal - don't specify region (as they are part of IAM)

### Load Balancers

3 types:
- application (layer 7, intelligent routing)
- network (used for extreme performance or static IPs)
- classic (old, used for test and development)

### Databases

- RDS (SQL, used for OLTP)
	- several engines
	- multi-AZ for disaster recovery
	- read replicas for performance
- Dynamo (No SQL)
- Redshift (used for OLAP)
- Elasticache (used to cache frequent queries)
- Neptune (graph databases)

### Autoscaling

- Create a group, allows deploying multiple EC2s behind load balancer
- Will scale with demand

### Domain Name System

- Computers use DNS to resolve IP addresses
- Route 53 is Amazon's DNS service, can be used to register domains and direct traffic
- Global service

### Elastic Beanstalk

- Quickly deploy app based on given code
- No worrying about infrastructure, health monitoring etc
- Fast deployment - if you don't know how to use AWS

### CloudFormation

- In contrast to EB, you use this if you know exactly what you're doing
- Create JSON/YAML template that describes instances - CF takes care of provisioning and configuring resources
- Infrastructure as code
- CloudFormation and EB are both free, but resources aren't
- EB is limited and not programmable - cloudformation is completely flexible nad programmable

### Important Global Services

- IAM
- R53
- CloudFront
- SNS
- SES

### Services Can be Used On-Prem

- Snowball
- Snowball Edge
- Storage Gateway
- CodeDeploy
- Opsworks
- IoT Greengrass

### CloudWatch

- Monitors AWS resources and applications on AWS
- Can monitor events every 5 minutes, or 1 minute with detailed monitoring
- Can create alarms which trigger performance

### Systems Manager

- Used to manage fleets of machines
- Software installed to let VM communicate (the agent) - either EC2 or on-prem
- Run Command used to install and patch software
- Integrates with CloudWatch for dashboard