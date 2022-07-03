# ACG CCP Practice Exam

(\*) was a question I was unsure about
~~strikethrough~~ is something I picked that was wrong
(+) is an answer I was wavering on - look out for these as trick questions

Question areas:
- identify service to be used for this use case:
	- content delivery globally, and speed it up (**cloudfront**)
	- provision isolated section of the cloud (**VPC**)
	- (\*) two software systems need to communicate, and need to ensure messages not lost between them - CloudWatch, SES, **SQS**, or SNS?
	- tracking usage (**AWS cost and usage report**)
	- (\*) database backups that need storing indefinitely, accessing within 6 hours - is S3, EFS, S3 Standard-IA, or **Glacier** cheapest? \[was unsure if Glacier was 6 or 12 hours retrieval - Glacier DA is 12, Glacier is less\]
	- (\*) developer trying to programmatically retrieve info from EC2 instance such as public keys, ip address, instance id - should they use CloudWatch logs, **instance metadata**, instance userdata, or instance snapshot?
	- migrating SQL server to new AWS account (**Database migration service**)
	- want to add autoscaling to add servers when usage reaches 70% threshold - how to trigger actions based on CPU utilization? ELB, **CloudWatch Alarms**, SNS, or EC2 Logs?
	- (\*) automate software deployments end to end - CodeCommit, **CodePipeline**, CodeBuild, or ~~CodeDeploy~~?
	- detecting and preventing DDoS (**Shield**)
	- identifying three CC models - **IaaS**, **Paas**, Hardware as a Service, **SaaS**
	- Load balancer to serve traffic at TCP and UDP layers - needs to handle millions of requests per second at very low latencies (**network load balancer**)
	- identify which *isn't* a check provided by TA: **elasticity**, security, cost optimisation, fault tolerance
	- how to implement elasticity in EC2 by adding and removing instances as needed? (**auto scaling**)
	- (\*) storing key-value pairs of users and high scores for gaming application - which is best option for this data type? RedShift, **DynamoDB** (+), S3, RDS MySQL (+)?
	- identify benefits of CC from a list
	- identify customer/AWS responsibilities from a list - e.g. customer networking, edge locations, availability zones, or **customer data**
	- (\*) company wants to run application for fixed length of 5 months, on an EC2 with no interruption - spot, dedicated (+), **on-demand**, or ~~reserved~~ (+)? \[This is not a long enough term to make reserved cost effective\]
	- (\*) store data for <= 10 years, archive as cheaply as possible, 12 hour retrieval - **glacier deep archive**, redshift, glacier, or S3 standard IA?
	- identify objects, people etc in scenes (**rekognition**)
	- nightly batch jobs that can be interrupted (**spot**)
	- consistent, high speed connection to AWS cloud that is better than internet-based connection (**direct connect**)
	- several EC2 instances in public subnet need internet access - what to configure as one step in granting access? VPC peering, API gateway, NAT gateway, or **Internet Gateway**?
	- what access creds to use in this situation? e.g. programmatic/CLI = **access key**
	- service providing central governance and management across accounts? IAM, CloudFormation, **AWS Organisations**, Systems manager
	- large number of buckets, automate a task - **resource groups**, IAM, tagging, IAM groups?
	- need reserved instances for 3-year project, but company may change all operating systems from windows to linux midway - what type should you purchase? automatic, standard, **convertible**, zonal
	- connect AWS cloud with on-prem data centre? IGW, VPC peering, IAM, **Virtual Private Gateway**
	- (\*) visualise, understand and identify trends for future charges, manage AWS costs and usage over time - CloudWatch, Trusted Advisor, **Cost Explorer**, ~~Cost and Usage Report~~ \[Cost Explorer lets you visualise understand and manage over time - cost and usage report is looking back at charges accrued, not looking forward and predicting\ ]
	- identify highly scalable cloud DNS service (**route 53**)
	- infrequently accessed data in S3 to move to glacier - bucket policy, **s3 lifecycle policy**, database migration service, cross origin resource sharing (CORS)
	- distribute traffic across zones and EC2 instances? **ELB**
	- need to set up a data warehouse (doesn't matter what for) - **Redshift**
	- (\*) want to setup loosely coupled architecture, send and receive messages, store if not consumed - CloudSearch, S3, **SQS**, or SES?
	- migrate large amounts of data at petabyte scale to AWS - API gateway, **snowball**, data pipeline, or DMS?
- identify core design principles:
	- e.g. deploying in multi-AZs, loose coupling
	- **not** tight coupling, planning ahead for capacity etc
	- (\*) company uploads large files to S3 using multipart upload - to which best practice does this adhere? decouple your components, implement elasticity, design for failure, **think parallel**
	- configuring permissions so that users can access only resources they need to do their jobs follows what principle? **principle of least privilege**
	- created large number of cloudformation templates in JSON format - how best to store? redshift, aurora, **DDB**, MySQL
	- (\*) configuring ALB -  how to ensure highly available architecture? multiple ELs for load balancer, more than one ALB, **configure LB to serve to multiple AZs**, set up cross-region load balancing
	- company has on-demand EC2s running to serve customers, pattern of two high demand points in the day, idle for rest of time - what is good way to optimise? ELB to scale in and out based on demand, script to stop instances when demand is low, **auto scaling group to scale in and out based on demand**, reserved instances instead of on-demand
	- (\*) your webserver in high demand, you add another EC2 to share the load - which principle is this? elasticity (+), durability, **horizontal scaling**, vertical scaling?
- billing:
	- what payment options will save most money? e.g. **all upfront**
	- what is most cost effective plan for full TA? **business**
	- (\*) track AWS costs on a detailed level - AWS organisations, AWS cloudtrail, ~~AWS cloudwatch~~, or **cost allocation tags**? \[selected CloudWatch as I thought cost allocation tags were made up - they track on a detailed level, once activated AWS uses them to organise resource costs on cost allocation report to make it easier for you to categorise and track costs - can have user defined and AWS generated tags\]
- identifying global services out of a list
	- e.g. **cloudfront**
	- **not** EC2, VPC, RDS
- security:
	- identify what used to access programmatically (**access keys**)
	- which service allows grouping users together and applying policies to group? **IAM**, **not** organisations or resource groups
	- what can you add as extra layer of protection into management console if passwords are stolen? **multi-factor authentication**
	- what steps can you take for creating and securing accounts? **create MFA for root account**, store root account creds in sharepoint, **add IP restrictions for all accounts**, grant admin access to all users, create functional groups for each department and use a common password for each group
	- how to setup virtual firewall? use **security group**
	- give app temporary access to AWS resources - **IAM role & have app assume role**, IAM policy and attach to app, store access key in S3 bucket and give application access to bucket, add application to group with appropriate permissions
	- most efficient way to assign permissions to multiple users in multiple departments? create policies per department, create IAM group for each department, attach policies to corresponding groups, then add each department's members to respective IAM group
	- (\*) what tool can you use to test IAM policies? ~~amazon inspector~~, cloudwatch, GuardDuty, **IAM policy simulator**? \[IAM policy another service I hadn't heard of - inspector examines applications and looks for vulnerabilities, but cannot examine individual policies - IAM policy simulator can test and troubleshoot identity-based policies, IAM permissions boundaries, organizations service control policies, and resource-based policies\]
- misc:
	- inherited application using EC2 Classic network - which Load Balancer works? **Classic**
	- identify advantages of moving to cloud from a list - **replace upfront capex with low variable costs**, **not** maintaining physical access but sharing responsibility, replacing variable with capital expensse
	- where to look for info re penetration testing EC2s? - **Customer Service Policy for Penetration Testing** - **not** customer agreement, IAM/JSON policy
	- (\*) need to launch a large number of instances into VPC - this number exceeds service limits for instances in VPC - what can you do? upgrade support plan to increase limit (+), use auto scaling and limit can be exceeded, **contact AWS and request a service limit increase** (+), nothing can be done
	- (\*) microsoft announced an OS patch. for a PAAS solution, who is responsible for applying patch? customer, either person can apply, customer for spot only, **AWS**
	- which is entirely AWS responsibility? **physical and environmental controls**, storing cloudformation in another region for disaster recovery, implementing IAM groups, patching of guest OS

Takeaways:
- cost and usage report not mentioned on ACG? cost allocation tags, IAM policy simulator also not mentioned specifically
- S3 lifecycle policy not mentioned on ACG but was mentioned in training earlier in year
- some services are worded differently to usual, but just use process of elimination to get rid of other ones
- some things you're not sure about may be hinted at in later questions - e.g. "which of these is a best practice?", followed by a later question saying "which of these best practices did the customer follow?"

Domain 3) Technology: 95% (33% of qns on this exam)
- define methods of deploying and operating
- define AWS global infrastructure
- identify core AWS services
- identify resources for tech support

Domain 1) Cloud Concepts: 100% (26% of qns on this exam)
- define cloud and its value proposition
- identify aspects of cloud economics
- list different cloud architecture principles

Domain 4) Billing and Pricing: 70% (16% of qns on this exam)
- compare and contrast various pricing models for AWS
- recognise account structures in relation to AWS billing and pricing
- identify resources available for billing support

Domain 2) Security and Compliance: 94% (25% of qns on this exam)
- define shared responsibility model
- define cloud security and compliance concepts
- identify AWS access management capabilities
- identify resources for security support