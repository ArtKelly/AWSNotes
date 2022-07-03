# Summary of Services

A brief summary of important services that might come up on the exam

## Core Services

### [[Chapter 2 - Cloud Concepts & Technology#S3 101|S3]]

Simple Storage Service
- Object-based storage, with objects in buckets
- Can be accessed globally
- Can be used to host static websites
- Access is controlled by bucket policies, access control lists, and IAM policies
- Multiple storage classes based on how often you need to retrieve data

### [[Chapter 2 - Cloud Concepts & Technology#EC2 101|EC2]]

Elastic Compute Cloud
- Virtual Server in the Cloud
- Allows quickly provisioning servers with a wide range of images and computing powers

### [[Chapter 5 - Advanced AWS Concepts#VPC Overview|VPC]]

A virtual data centre in the cloud, dedicated to you and customisable. Can also be used to extend an existing datacentre with a VPN connection.

**(Free)**

### [[Chapter 2 - Cloud Concepts & Technology#Let's Start to Cloud Identity Access Management IAM|IAM]]

AWS' core service for managing permissions for users and groups
- Allows assigning users to groups
- Allows creating policies that define what actions can be performed by users and groups on which resources
- Allows auditing via credential reports

**(Global, Free)**

### [[Chapter 5 - Advanced AWS Concepts#Lambda|Lambda]]

Serverless compute service for executing code in response to events such as HTTP request and Amazon API calls.

## Databases & Content Delivery

### [[Chapter 2 - Cloud Concepts & Technology#Relational Databases|RDS]]

Amazon's relational database service

### [[Chapter 2 - Cloud Concepts & Technology#Non Relational Databases|DynamoDB]]

Amazon's non-relational database service

### [[Chapter 2 - Cloud Concepts & Technology#Processing|Redshift]]

Amazon's data warehousing service
- data warehousing is for processing large amounts of data away from production DB

### Database Migration Service (DMS)

Used for migrating existing database to AWS.

### [[Chapter 2 - Cloud Concepts & Technology#ElastiCache|ElastiCache]]

Caching service used for storing common queries and reducing load on production database

### [[Chapter 2 - Cloud Concepts & Technology#CloudFront|CloudFront]]

AWS' Content Delivery Network
- Uses a network of edge locations to cache content

**(Global)**

### Amazon Neptune

Amazon's Graph Database Service

## Networking & Performance

### [[Chapter 2 - Cloud Concepts & Technology#Let's Use a Load Balancer|Load Balancers]]

Distribute traffic automatically between targets
- can be EC2s, IPs, Lambdas etc

### [[Chapter 2 - Cloud Concepts & Technology#Autoscaling|Autoscaling]]

Automatically adjusts number of instances in a group
- can be used in combination with Load Balancers for fault tolerant webservers

**(Free)**

### [[Chapter 5 - Advanced AWS Concepts#Direct Connect|Direct Connect]]

Service for connecting an on-premise datacentre directly to AWS.

## Infrastructure as a Service

### [[Chapter 2 - Cloud Concepts & Technology#Cloudformation|CloudFormation]]

Service for deploying infrastructure as code

**(Free)**

### [[Chapter 3 - Billing & Pricing#Quickstart|Quickstart]]

Allows quickly deploying a single-account solution for a specific technology.

### [[Chapter 3 - Billing & Pricing#Landing Zone|Landing Zone]]

Allows deploying a multi-account AWS structure using best practices.

## Web Applications & PAAS

### [[Chapter 2 - Cloud Concepts & Technology#Buying a Domain Name|Route 53]]

Amazon's DNS Service
- allows buying domain names
- allows managing flow of traffic

**(Global)**

### [[Chapter 2 - Cloud Concepts & Technology#Elastic Beanstalk|Elastic Beanstalk]]

Allows quickly deploying web apps without configuring underlying technologies

**(Free)**

### Lightsail

Amazon's Virtual Private server service - used for simple web applications with pre-configured dev stacks (LAMP, MEAN etc), websites (with Wordpress, Joomla etc), launching business software (open source and commercial software), and dev/test environments (disposable sandboxes etc)

## Security, Identity & Compliance

### [[Chapter 4 - Security In The Cloud#AWS WAF Web Application Firewall|WAF]]

Web Application Firewall - used to detect and prevent hacking attempts at application layer.

### [[Chapter 4 - Security In The Cloud#AWS Shield|Shield]]

Used to detect and prevent DDoS attacks.

### Firewall Manager

Beyond CCP scope - allows deploying/managing firewalls across multiple accounts.

### [[Chapter 4 - Security In The Cloud#Amazon Inspector|Amazon Inspector]]

Used for auditing security on an EC2 instance.

### [[Chapter 4 - Security In The Cloud#Trusted Advisor|Trusted Advisor]]

Used for auditing security across a whole AWS account, as well as performance, cost optimisation, and fault tolerance.

**(Global)**

### [[Chapter 4 - Security In The Cloud#AWS KMS Key Management Service|KMS]]

Amazon's encryption, decryption, and key management service - it runs on shared hardware - allows encrypting S3 objects, database passwords, parameters in parameter store.

### [[Chapter 4 - Security In The Cloud#CloudHSM|CloudHSM]]

Similar to KMS, but on dedicated hardware.

### [[Chapter 4 - Security In The Cloud#Parameter Store|Parameter Store]]

Stores all kinds of secrets that can be used with other AWS services. Limited to 10,000 parameters.

**(Free)**

### [[Chapter 4 - Security In The Cloud#Secrets Manager|Secrets Manager]]

Just like parameter store, but unlimited and paid. Also integrates with services like CloudFormation, and can generate random passwords.

### [[Chapter 4 - Security In The Cloud#GuardDuty|GuardDuty]]

ML-powered intrusion and anomaly detection system that monitors your AWS account for suspicious activity.

### [[Chapter 4 - Security In The Cloud#Security Hub|Security Hub]]

Central management console for aggregating security reports from multiple accounts. Includes alerts and findings from GuardDuty, Inspector, Macie, IAM Access Analyzer, and Firewall Manager.

### [[Chapter 4 - Security In The Cloud#Macie|Macie]]

Automatically detects and protects PII stored in S3. Can be used to analyse S3 data and CloudTrail logs.

###  IAM Policy Simulator

Service that can test and troubleshoot identity-based policies, IAM permissions boundaries, organizations service control policies, and resource-based policies

## Management & Governance (incl. Auditing)

### [[Chapter 2 - Cloud Concepts & Technology#AWS Systems Manager|Systems Manager]]

Used for running commands remotely across a large number of EC2s.

### [[Chapter 3 - Billing & Pricing#What is CloudTrail|CloudTrail]]

Amazon's API monitoring service used for auditing actions within the whole cloud environment. Extra details in [[Chapter 4 - Security In The Cloud#AWS Inspector vs AWS Trusted Advisor vs CloudTrail]]

### [[Chapter 2 - Cloud Concepts & Technology#CloudWatch 101|CloudWatch]]

Monitoring service for AWS services and applications running on AWS.

### [[Chapter 4 - Security In The Cloud#Control Tower|Control Tower]]

Tool for centrally deploying multiple AWS accounts and applying security policies to them.

### [[Chapter 3 - Billing & Pricing#What is AWS Organisations|AWS Organisations]]

A way of managing several AWS accounts from a central account. Uses Organisational Units to group accounts, and Service Control Policies (SCPs) to control permissions for accounts and OUs.

### [[Chapter 3 - Billing & Pricing#Consolidated billing Practical Example|Consolidated Billing]]

Part of AWS Organisations - allows billing to be tracked and paid from a central paying account.

**(Free)**

### [[Chapter 3 - Billing & Pricing#What are Tags|Tags]]

Tagging resources allows easy grouping of resources by custom categories.

#### Tag Editor

Allows searching by tags and adding additional tags to resources.

**(Global)**

### [[Chapter 3 - Billing & Pricing#Resource Groups|Resource Groups]]

Allows grouping resources together by tags and applying automation to the group using Systems Manager

### [[Chapter 2 - Cloud Concepts & Technology#Service Health Dashboard|Service Health Dashboard]]

Shows status checks for specific services across all regions.

### [[Chapter 2 - Cloud Concepts & Technology#Personal Health Dashboard|Personal Health Dashboard]]

Whereas Service Health Dashboard shows all services, Personal Health Dashboard only shows ones relative to your account - proactive notifications, service status for services you use.

## Cost Management

### [[Chapter 3 - Billing & Pricing#AWS Budgets|AWS Budgets]]

Allows setting budgets for your account and setting up alarms when they are reached - a predictive service, setup in advance (before costs incurred).

### [[Chapter 3 - Billing & Pricing#AWS Cost Explorer|AWS Cost Explorer]]

Allows retrospective analysis of costs, after they've been incurred.

### [[Chapter 4 - Security In The Cloud#Athena|Athena]]

Interactive, serverless query service for querying data stored in S3 using standard SQL.

## Machine Learning

### [[Chapter 5 - Advanced AWS Concepts#Lex|Lex]]

Amazon's conversational chatbot service. Can be text- or speech-based

### [[Chapter 5 - Advanced AWS Concepts#Polly|Polly]]

Polly is a text-to-speech service available in multiple languages, genders, and accents.

### [[Chapter 5 - Advanced AWS Concepts#Transcribe|Transcribe]]

Speech-to-text service used for generating transcripts, subtitles etc

### [[Chapter 5 - Advanced AWS Concepts#Rekognition|Rekognition]]

Scene analysis tool for identifying objects and doing facial analysis.

## Misc

### API Gateway

Amazon service for building APIs (application programming interfaces)

### Elasticsearch

A managed Elasticsearch Service with built-in Kibana for searching data

### SNS

Amazon's Simple Notification Service, for sending messages both application to application (A2A) and application to person (A2P)

**(Global)**

### SES

Simple Email Service - cost effective, flexible and scalable email service to allow devs send mail from any application

**(Global)**

### Snowball

On-prem service for uploading large amounts of data to AWS when you don't have a sufficiently fast internet connection.

#### Snowball Edge

Like snowball, but provides compute power also - i.e. lets you run lambdas locally without an internet connection.

### Storage Gateway

Like Snowball - on prem solution for caching datacentre files - if internet connection is lost, they are still available locally.

### CodeDeploy

Fully managed deployment service that automates software deployments to variety of compute services - EC2, Fargate, Lambda etc, and on-prem servers.

### Opsworks

Another service for automated deployment of code and apps to EC2 or on-prem webservers - more focused on devops

**(Free)**

### File Gateway

Acts as an access point to large data repositories for latency-sensitive applications. Works with S3 (S3 File Gateway), and also Windows File Server (FSx file gateway). Allows retrieving files from S3 using industry-standard protocols such as Network File System (NFS) and Server Message Block (SMB). Essentially a file system mount on S3.

### Elastic File System

File storage service for use with EC2. EFS provides file system interface, file system access semantics (e.g. consistency, file locking), and concurrently-accessible storage for up to thousands of EC2 instances.

## SQS

Simple queueing system - message queue for sending and receiving messages, stores if not consumed immediately.

## Code Pipeline

Fully managed continuous delivery service - helps you automate release pipelines for fast and reliable application and infrastructure updates. Automates build, test and deploy phases of release process every time there is a code change, based on release model defined by you. Enables rapid and reliable delivery of features and updates.