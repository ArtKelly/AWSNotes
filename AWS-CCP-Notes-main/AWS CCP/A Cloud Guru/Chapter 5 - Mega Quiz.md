# Chapter 5 Mega Quiz

Interesting questions
- which service acts as a file system mount on S3? **File Gateway** - we weren't taught about this in CG
- how will dev team be billed if they have 4 on-demand EC2 instances, when they are in an organisation with an account using 3/5 reserved instances (assume all in same AZ, same type)? **Charged for 2 at on-demand price, 2 at reserved price**
- which of the following are good cloud design principles? **assume everything will fail**, **disposable resources**, **infrastructure as code**, **scalability**, limit number of 3rd-party services, tightly-coupled components, treat servers like pets not cattle
- best strategy for ensuring global availability at all times? deploy to all AZs in home region, multi-AZ, multi-VPC in two AWS regions, or **multi-region**
- which of following support services do all accounts receive as standard? 24/7 phone/chat, TAM, **billing support**, technical support
- which of following is *not* a feature of AWS organisations? grouping of accounts into OUs as part of hierarchy, AWS accounts having benefit of consolidated billing, **granular configuration of security groups within VPCs**, hierarchical based control over groups of IAM users and roles
- which services to use if you'd like to be notified when crossed a billing threshold? AWS cost and usage reports, trusted advisor, **CloudWatch**, **AWS Budgets** - cost and usage reports are retrospective breakdown, don't provide alerts

Simple questions:
- comparing numbers of AZs, regions, ELs
- generally identifying services by use case e.g. data warehousing (redshift), recommendations for environment (trusted advisor), running code without worrying about infrastructure (lambda), database migrations (DMS), processing large data sets (Elastic Map Reduce), identify managed AWS DB service (aurora), host a file publicly accessible from anywhere in world (S3 - via URL)
- identifying correct definitions for basic concepts e.g. regions
- identify things from a list AWS/customer is responsible for under shared model e.g. datacentre security, customer data
- identify pricing plans for use case e.g. 90 hours of computing time, no deadline, and can be stopped and started (spot instance)
- identify compute services from an assorted list
- identify support plans offering a certain service e.g. business and enterprise offering unlimited support cases and contacts