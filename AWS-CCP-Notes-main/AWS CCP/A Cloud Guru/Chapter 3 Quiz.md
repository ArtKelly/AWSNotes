# Chapter 3 Quiz

Interesting questions:
- which of following is not a fundamental AWS charge? **data-in**, storage, compute, or data-out
- which of following AWS services are free to use? RDS, **CloudFormation**, EC2, EBS, S3, **Auto-scaling**, **IAM**, **Elastic Beanstalk**, **VPC**, Route53
- which of following components are billed for Amazon RDS instances? Standby time, **storage**, data transfer incurred in replicating data between your primary and standby in a multi-az DB instance deployment, **I/O requests for Amazon RDS magnetic storage**, **DB instance hours** - not charged for replicating data (but secondary instances do cost money, which is why I picked it) - RDS billed on storage capacity provisioned (pro-rated if scaled), number of I/O requests (for magnetic storage only), and instance class
- Which AWS support plan provides enhanced technical support **only** during business hours via email? **Developer**
- Choose features of consolidated billing - **account charges tracked individually**, charging based per VPC, **multiple standalone accounts combined and may reduce your overall bill**, **a single bill issued containing charges for all AWS accounts**
- Which two best describe resource groups? **Colletion of resources that share one or more tags**, collection of resources of same type that share one or more tags or portions of tags, **collection of resources that are deployed in same AWS region, and that match criteria specified in group's query**, collection of resources of same type that are deployed in same AZ - basically, groups don't have to be same type (EC2, S3 etc) but do have to be in same region

Simple questions:
- identify valid pricing options
- identify default max linked accounts
- identifying which pricing plans save and how
- identifying response times