# Chapter 4 - Security in the Cloud

Security & Compliance in AWS

## Compliance on AWS & AWS Artifact

How do we know it's compliant?
- safe to do credit card transactions?
- safe to store health data?

[https://aws.amazon.com/compliance](https://aws.amazon.com/compliance)
- lists the various compliance programmes by country
- payment standards, ISO, HIPAA, PCI DSS, GDPR compliance etc
- AWS is compliant up to infrastructure layer - does not mean if you host on AWS you are automatically compliant - you must complete a gap audit (checking things like security groups, secure RDS instances etc) - shared responsibility
- can get copies of these reports via the webpage to give to auditors

### Artifact
- can also get reports via Security, Identity & Compliance > Artifact
- comprehensive list of access control docs relevant to security and compliance in cloud
- basically provides various compliance guides and documentation for different schemes

## Shared Responsibility Model

### Exam Tips

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

### Overview

Very important concept for CCP
AWS manages security of the cloud - security *in* the cloud is the responsibility of the customer
Customers retain control of what security they implement to protect their own content, platform, applications, systems and networks, no differently than they would in an on-site datacentre

Amazon responsible, say, for securing datacentres themselves
You are responsible for securing your EC2 by applying patches, for example

![[Pasted image 20210518110436.png]]

AWS:
- regions, AZs, ELs
- the hardware inside these regions
- computer, storage, database, networking
	- where 'database' is the database that stores *your* data
	- software e.g. the hypervisor - for example patching operating system, RDS, not letting you login as the operating system on RDS

Customer:
- client-side data (how encrypted), server-side data (e.g. in S3), networking traffic protection (encryption, integrity etc)
- operating system (e.g. EC2 - AWS responsible for RDS, but they can't log into your EC2), network and firewall config
- platforms, applications, IAM - i.e. not publishing secret access key on github - that's your fault, not AWS'
- protecting customer data

[Read about the model](https://aws.amazon.com/compliance/shared-responsibility-model/) before the exam
- helps relieve operational burden as AWS manages host operating system and virtualization layer, as well as physical datacentre security
- customer assumes responsibility for management of guest OS - patching OS, and other applications software; also configuration of AWS-provided firewall
- basically, AWS responsible for guest OS on EC2 and below, us responsible for guest OS upwards
- whenever some service runs on an OS (RDS, S3), AWS responsible for underlying OS (as customer doesn't have access to it)
- basically - if asked where you need to patch, that's EC2 - AWS responsible for S3/RDS - you're responsible for the data that is stored on those services, and should be secured when being transmitted etc

## AWS WAF & AWS Shield

### Exam Tips

- WAF designed to stop hackers doing things like XSS on application layer
- AWS Shield is a DDoS mitigation service designed to stop DDoS attacks

### AWS WAF (Web Application Firewall)

Web application firewall that helps protect your web apps from common web exploits that could affect application availability, compromise security, or consume excessive resources

OSI Model
- 7 (8) layers
- start at layer 1 - hardware
- goes all way up to 7 - application
- WAF sits at layer 7 - inspects your web traffic, looks for people doing malicious things
- normal firewalls operate at layer 4 (transport layer) - can see traffic from application layer

Example:
- attacker finds a vulnerability in a wordpress site (XSS, SQLi etc)
- sends this to the load balancer
- load balancer passes it to EC2 instance, EC2 is compromised
- if WAF sits in front of ELB, it decides not to send it on to EC2s - detects the malicious entities in the traffic/code

### AWS Shield

Managed distributed denial of service (DDoS) protection service that safeguards web applications running on AWS

Where WAF protects against hackers, Shield protects against DDoS
Overloading site with a large amount of traffic to the point it stops responding

AWS Shield provides always-on detection and automatic inline mitigations that minimise applicaiton downtime and latency - basically, there is no need to engage/enable/interact with AWS Support to benefit from DDoS protection

Two tiers of AWS Shield: Standard and Advanced
- Standard has active monitoring, DDoS mitigations - enabled and free by default
- Advanced also inclides automated layer 7 monitoring, additional DDoS mitigation capacity, layer 3/4 attack notification and attack forensic reports, layer 3/4/7 attack historical report, incident management during high severity events, custom mitigations during attacks, post-attack analysis
- Crucially, advanced offers cost protection - if you do get DDoSed, don't have to pay for R53, CloudFront and ELB DDoS-related costs
- Advanced is $3000/month

### Console

Security Identity & Compliance > WAF & Shield
- Firewall Manager allows managing WAF across multiple accounts (beyond CCP scope)
- WAF -> configure firewall (covered in Security Associate)
- Shield Advanced -> Activate

## AWS Inspector vs AWS Trusted Advisor vs CloudTrail

### Exam Tips

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

### Amazon Inspector

Automated security assessment service - helps improve security and compliance of applications deployed on AWS
Automatically assesses applications for vulnerabilities or deviations from best practices
After performing assessment, Inspector produces detailed list of security findings prioritised by severity
Findings can be reviewed directly or as part of assessment reports available via Inspector console or API

Basically, an agent installed on EC2 that looks for common vulnerabilites, for example from Centre for Internet Security
Checks for patches etc
Associate Inspector with EC2 - inspects environment

### Trusted Advisor

Advises about multiple aspects of AWS and best practices

Know default services available to you:
- security monitoring
- service limits

Other services only available to business/enterprise support tier:
- cost optimisation
- performance
- fault tolerance

#### Overview

Not just security - online resource to help you reduce cost, increase performance, and improve security by optimising AWS environment
Real time guidance to help provision resources based on AWS best-practices
Takes into account cost optimisation, performance, security, and fault tolerance

Inspect **entire** AWS environment - not just EC2
Generates a report

Two flavours
- core checks and recommendations (**free**)
- full trusted advisor (business and enterprise companies only)

Understand what it can check for:
- cost optimisation: how to best optimise AWS cost (not available by default - business/enterprise tier)
- performance: also limited to business/enterprise
- security: EBS public snapshots and RDS public snapshots are free, as well as security groups, IAM user, bucket permissions, MFA usage etc
- fault tolerance: also limited to business/enterprise
- service limits: monitor how close you are to hitting cap for services

### CloudTrail vs CloudWatch

- CloudWatch monitors performance
- CloudTrail monitors API calls in AWS platform
	- Like a CCTV camera
	- Record everything goign on in environment
	- Increased visibility by recording console actions and API calls
	- Identify which users and accounts called AWS, source IP address, and when calls occurred
	- All saved into S3

### In the Console

Services > Management & Governance > CloudTrail - creating trails beyond scope
Services > Management & Governance > Trusted Advisor
Services > Security, Identity & Compliance > Inspector

**Trusted Advisor**

Scans environment as soon as launched
Checks services across world
- looks for open ports
- check open access permissions on buckets
- IAM best practices etc

Upgrade support plan to unlock all of TA

**Inspector**

Has to be installed on EC2 instances
Can set it up to scan weekly, or a one-off

## CloudWatch vs AWS Config

### Exam Tips

- CloudWatch monitors performance
- AWS Config monitors configurations of AWS Resources
- If asked about settings changing, such as security group rules, think AWS config
- If asked about performance, such as number of connections to RDS, think CloudWatch

5 services may be asked about in scenario-based questions:
- Inspector
- Trusted Advisor
- CloudTrail
- CloudWatch
- AWS Config

### Overview

Exam gives scenario-based questions - asked which service should use in each scenario

CloudWatch all about performance of AWS resources
- used a lot with EC2 - host reports to cloudwatch
- host-level metrics - CPU, network, disk utilisation, health status checks
- custom metrics - write a script to send stuff back to CloudWatch - monitor RAM, storage, number of people logged in

**AWS Config**

- Provides detailed view of configuration of AWS resources in AWS account
- Includes how resources are related to one another and how they were configured in the past so that you can see how the configurations and relationships change over time
- Basically monitors settings of AWS environment - e.g. security group firewall rules - Config will detect a change in the security group rules e.g. making a port open to world

## Penetration Testing

Understand what you can and can't do with AWS Penetration Testing

What is it?
- a simulated cyber attack against your computer system to check for exploitable vulnerabilities

You *can* carry out penetration tests against your AWS Infrastructure without prior approval for eight services:
- Amazon EC2 instances, NAT gateways, and Elastic Load Balancers
- Amazon RDS
- Amazon CloudFront
- Amazon Aurora
- Amazon API Gateway
- AWS Lambda & Lambda Edge Functions
- Amazon Lightsail Resources
- Amazon Elastic Beanstalk Environments

Prohibited acitivities:
- DNS zone walking via R53 hosted zones
- Distributed denial of service (or simulated)
- Port flooding
- Protocol flooding
- Request flooding (login request/API request)

For any other simulated events, contact: aws-security-simulated-event@amazon.com or visit https://aws.amazon.com/security/penetration-testing

## AWS KMS vs HSM

### Exam Tips

- **AWS KMS** is Amazon's encryption, decryption, and key management service - it runs on shared hardware
- **CloudHSM** does pretty much everything KMS does, but uses dedicated hardware - better for compliance

### AWS KMS (Key Management Service)

Regional service that does secure key management and encryption and decryption of data
Manages your customer master keys - used for encryption and decryption
Ideal for S3 objects, database passwords, API keys stored in Systems Manager Parameter Store
If asked on exam about S3 encpryption (or otherwise), think of KMS
Encrypt and decrypt data up to 4Kb in size
Integrated with most AWS services - mostly around S3

Key difference with HSM - KMS is on **shared hardware**
Similar to EC2 - on shared physical hardware with other customers
Isolated, but not dedicated to you

### CloudHSM

Does everything KMS does + more
Dedicated hardware security module (HSM)
Not multi-tenant - underlying hardware not shared (but more expensive)
Compliant with FIPS 140-2 Level 3 - US encryption standard
Single-tenant, dedicated hardware, multi-AZ cluster
Only need this if you need dedicated hardware/compliance

Certified security specialty course has a deep dive if interested
AWS Cloud Security very well paid...

## Parameter Store vs Secrets Manager

Both places to store passwords

### Exam Tips

- **Parameter Store** is free, but limited to 10,000 parameters - can be encrypted
- **Secrets Manager** does everything Parameter store does with no limit (but costs money) - can also generate random passwords and automatically use service passwords when integrated with CloudFormation

### Parameter Store

Part of AWS Systems Manager (SSM)
Secure serverless storage for configuration and secrets:
- passwords
- database connection strings
- can be stored encrypted (with KMS) or plaintext
- can set TTL to expire values
**Free** - but a limit of 10,000 per account

### Secrets Manager

Larger organisations want Secrets Manager
- charge per secret stored and per 10,000 API calls

Automatically rotate secrets
Can apply new key/password in RDS automatically (for example, in a CF template)
Can generate random secrets (via SDK or command line)

## GuardDuty

Might be asked a scenario - pick a service to fix the problem

GuardDuty uses machine learning algorithms for anomaly detection, and third-party data to monitor and protect your AWS account
For example, look for dodgy activity in CloudTrail logs
One-click to enable (30-day trial)
On a per-account basis

Input data includes:
- CloudTrail event logs
- VPC Flow logs
- DNS logs

## Control Tower

Easiest way to set up and govern a new, secure, multi-account AWS environment
Allows provisioning multiple AWS accounts in just a few minutes
Those accounts will conform to company policies
Used for large enterprises with multiple AWS accounts
For example, allowing a new dev to be granted access to accounts that allow deploying certain resources in test and dev - e.g. no multi-AZ instances in dev

## Security Hub

Imagine large enterprise with huge AWS landscape, 10s of thousands of AWS accounts - how do you check for an opened port when auditing?
Using Trusted Advisor to log into everything takes time

Security Hub gives comprehensive view of security alerts across multiple accounts - single places that aggregates, organises and prioritises your security alerts and findings from multiple services across multiple accounts
- these could include GuardDuty, Inspector, Macie, IAM Access Analyzer, Firewall Manager

## Compromised IAM Credentials

Real-world situation - hard-coded access keys published to GitHub - bots that go and scan repos for keys

How to deal with it?
1) Determine what resources those credentials have access to - full access? partial? this is where POLP comes in
2) Invalidate credentials - go into IAM, delete creds to stop people using them
3) Consider invalidating any temporary security credentials that might have been issued *using* those credentials
4) Restore appropriate access to that user (and tell them off)
5) Review access to AWS account - make sure no one has logged in

## Athena vs Macie

### Exam Tips

- Athena: interactive query service
	- queries data in S3 using standard SQL
	- serverless
	- commonly used to analyse log data
- Macie: auditing/security tool for identifying and protecting PII in S3
	- can also analyse CloudTrail logs for suspicious API activity
	- interactive dashboards, reports and alterting
	- great for PCI-DSS compliance

### Athena

Interactive query service which enables you to analyse and query data located in S3 using standard SQL
Can be any type of data - might be network traffic, VPC flow logs, CloudTrail, logging data
Athena lets you create an SQL query and run it over S3 - for example, logs from a certain VPC
Serverless, nothing to provision
You pay per query / TB scanned
No need to setup complex Extract/Transform/Load (ETL) processes to make the data processable
Works directly with data in S3
Doesn't have to be security - could be mining a lake etc

Uses:
- log files in S3 e.g. ELB logs, S3 access logs
- Generate business reports on data stored in S3
- Analyse AWS cost and Usage reports
- Run queries on click-stream data

### Macie

What is PII? Personally Identifiable Information
- used to establish an individual's identity
- could be exploited by criminals, used in identity theft and fraud
- many types: address, email, SSN, DoB etc

Macie is a security service that uses Machine Learning and NLP to discover, classify and protect sensitive data stored in S3
- uses AI to recognise if S3 objects contain sensitive data like PII
- outputs via dashboards, reporting and alerts
- works directly with data in S3
- can also analyse CloudTrail logs
- Great for PCI-DSS and preventing ID theft

## Summary

### AWS Artifact

- AWS Artifact is used to retrieve compliance reports for bodies all around the world

### Shared Responsibility Model

- AWS always responsible for security **of** the cloud - things like hardware, global infra, datacentres, regions, AZs, ELs - also for the services that sit on top, e.g. compute, storage, database, networking and any software sitting on top of that stack - all the way up to layer 7 in some circumstances (RDS for example - OS + patching MySQL)
- Customer responsible for security **in** the cloud - patching EC2, patching applications that run on your EC2 - securing S3 with bucket policies and encryption
- In summary, if you can do it yourself (e.g. in console), you're probably responsible; if you can't control or configure it, it's probably AWS

### AWS WAF & Shield

- **AWS WAF** is a Web Application Firewall, designed to stop hackers
- **AWS Shield** is a DDoS mitigation service designed to stop DDoS attacks (free by default, advanced $3k/month)

### AWS Auditing Tools

- **Inspector** used for inspecting EC2 instances for vulnerabilities
- **Trusted advisor** inspects your whole EC2 account for security issues, as well as for fault tolerance, cost optimisation, and performance
- **CloudTrail** increases visibiity into user and resource activity by recording Management Console actions and API calls; data includes source IP address, time and date, account and IAM user

### Athena & Macie

- **Athena** is an interactive query service that can query S3 with common SQL; completely serverless
- **Macie** is an AI tool used for analysing data in S3 and identifying PII; it can also analyse CloudTrail logs; includes dashboards, reports, and alerting; good for PCI-DSS compliance