# Chapter 5 - Advanced AWS Concepts

## AI Services: Lex, Polly, Transcribe, Rekognition

### Lex

Alexa product is powered by the Lex service
Service allows building conversational chatbots
These can be powered either via voice or text
Hear chatbot on the exam, think Lex

### Polly

Text to lifelike voice
Polly generates Alexa's voice - Lex processes what you say, and Polly returns it
Can choose from a number of languages, whether the voice is male or female, and what accent to render the voice in

### Transcribe

Converts speech into text
Can be great for generating subtitles or getting transcripts of interviews, speeches, and more
Used by cloud guru for subtitles and transcripts
Used to have high error rate but okay now

### Rekognition

Convert images into tags/text
Upload an image - rekognition tell you what it thinks the image is with a certain degree of confidence
Can be used with lots of apps - e.g. taking photo of a plant, app tells you what the plant is

### In the Console

See Services> Machine Learning

**Polly**

Type into box, choose language, region, voice etc
Can take text or [SSML](https://cloud.google.com/text-to-speech/docs/ssml) (speech synthesis markup language)
Can it integrate with other apps?

**Rekognition**

- Scene detection: identifies objects
- Facial analysis: age range etc
- Face comparison

## EC2 Licensing

Remember [[Chapter 3 - Billing & Pricing#EC2 Pricing Models]]

With any question that asks about special licensing requirements, think of *Dedicated Host*.

EC2 dedicated host is a physical server with EC2 instance capacity fully dedicated to your use. Allows you to use your existing per-socket, per-core, or per-VM software licenses (such as Windows Server, Microsoft SQL Server, SUSE Linux Enterprise Server)

## Different Compute Services

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

## VPC Overview

Provisioning resources occurs in default VPC - get one per region whenever you start an account

**What is VPC?**

Amazon Virtual Private Cloud - lets you provision a logically isolated section of the AWS cloud where you can launch resources in a virtual network defined by you.

Can deploy all sorts of resources to a VPC - EC2, S3, DDB - basically where you deploy your instances.

You have complete control over virtual networking environment - IP address ranges, creation of subnets, which subnets are public/private

Essentially a **virtual datacentre in the cloud** - you make the rules, decide what goes in and out

Customisable configuration
- can create public-facing network zone for web servers that have access to internet
- can place backend systems like databases/application servers in a private network zone with no internet access

Can connect VPC to an existing VPN via a hardware virtual private network connection between corporate data centre and VPC, leveraging AWS cloud as an extension of corporate data centre.

Solutions architect takes deep dive into VPC.

## Connecting On-Premises to AWS

### VPN
- create a hardware VPN connection between corporate datacentre and AWS VPC
- essentially extend a network out to a remote location - gives you same IP address range at home as you would in your office

### Direct Connect
- cloud service solution that makes it easy to establish a dedicated network connection from your premises to AWS
- it is a direct, physical line in to AWS
- establish private connectivity between AWS and your data center, office, or colocation environment
- in many cases, can reduce network costs, increase bandwidth throughput, provide a more consistent network experience than internet-based connections
- traffic is also not traversing the wider internet - increase security

### VPN Over Direct Connect
- ultimate security - not only a dedicated line to AWS, but all your taffic to and from AWS is encrypted over Direct Connect connection using a VPN

## Lambda

### Exam Tips

- Lambda **scales out** (not up) automatically
- Lambda functions are independent (1 event = 1 function)
- Lambda is serverless
- Know how Lambda is priced (per invocation and per execution time)
- You can have multiple versions of your code inside Lambda
- Understand shared responsibility model - you are responsible for your code and the version of the language it runs on, Amazon for everything else

### Overview

Every time you speak to an Alexa or Echo, you're directly interacting with Lambda
Just by using Cloud Guru site, you're interacting - whole platform is serverless, all Lambda functions interacting via API Gateway

**Brief History of Cloud**

Used to be physical machines that people go out and purchase - rack them, do cabling, install antivirus and applications
10-20 days to setup
Infrastructure as a service came in in 2006 - EC2 launched, IAAS changed the world
Tech startups now much easier
Then PAAS came out - Elastic Beanstalk etc
Then containers - e.g. docker - place to store and deploy code where everything is standardised - can run the code on any platform anywhere in the world and it will run the same way
But you have to manage containers - Serverless/Lambda is the ultimate abstraction layer - we store our code, and it gets invoked every time it's triggered - don't have to worry about *anything* infrastructure wise - **just the code**

 ### What is Lambda?

The ultimate abstraction layer - you no longer have to worry about:
- data centers
- operating systems
- assembly code
- protocols
AWS manage:
- hardware, application layer, AWS APIs
- AWS Lambda itself
- High-level languages Lambda runs on

Compute service that lets you upload a **Lambda function**
- AWS takes care of provisioning and managing servers you  use to run the code
- You don't have to worry about operating systems, patching or scaling

It is an **event-driven** compute service that can run code in response to events
- for example, these events could be changes to data in an S3 bucket or a DDB table
- E.g. when uploading image and text to an S3, it overlays image with text and saves it
- basically, a compute service to run your code in response to HTTP requests using Amazon API gateway or API calls made using AWS SDKs

### Lambda Architecture

Traditionally, a load balancer (e.g. ELB) -> webservers (EC2) -> backend database (e.g. RDS)
Instead of hitting load balancer, you hit API gateway:
- API call -> API gateway -> Lambda
- Lambda can then store things in RDS/DDB (true serverless is DDB - just paying for execution time)
- traditionally, you have EC2, RDS etc up and running constantly
- with serverless, you only pay for stuff exactly when it gets used - when making API call, triggering Lambda function, saving data to DDB
- saves a fortune - ran CG for free for 2 years as everything was within free tier - lets you scale extremely quickly

### Basics to know for exam

#### Supported Languages

- Node.js
- Java
- Python
- C#
- Go
- PowerShell

#### Pricing

1) Number of requests (first million are free, then $0.20/request)
2) Duration (calculated from time your code begins executing until it returns or otherwise terminates, rounded up to nearest 100ms) - price depends on amount of memory allocated to your function (charged $0.00001667/GB-second)

#### Version Control

- You can use version control with Lambda to have multiple versions of code
- Can roll back code at any time to restore a previous version

#### Shared Responsibility Model

- You're responsible for code nad the version of programming language that is running
- Amazon responsible for all hardware, operating systems, security patching of stack, antivirus, datacentre security
- Not responsible for much

### What sets Lambda apart?

- Get rid of traditional servers
- Scales automatically and continuously - don't need to setup scaling events etc
- Super cheap

### In the Console

- Write a function
- Give it an execution role
- Test it using test events
- Can link up to CloudWatch for logging