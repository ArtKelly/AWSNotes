# Chapter 2 Quiz

Interesting questions:
- Which pricing best for long-term workloads with predictable usage patterns? **Reserved instances**
- CloudFront Distribution is a link between an origin server and a domain name, which CloudFront automatically assigns - **True** (S3 -> R53 etc - CF uses this to identify object stored in origin server
- Identifying cloud expenses - saying that capital is not one of them
- Lightsail is FAAS, IAAS, SAAS, or PAAS? Wasn't sure what service was - it's **platform as a service** - used for hosting websites and appications, don't have to worry about procurement, maintenance etc
- Which of following R53 policies allow you to a) route data to a second resource if first is unhealthy, and b) route data to resources that have better performance? Failover-routing and latency based routing (other options were geolocation routing, geoproximity routing, simple routing)
- At least 2 AZs per region
- T/F - objects stored in S3 in single central location within AWS? **False** - multiple servers, multiple facilities
- T/F - general rule AWS recommends S3 ACLs for access control? **False** - bucket policies or IAM policies for general rule. ACLs are legacy access control predating IAM. They may work and no need to change. Some scenarios require ACL, for example bucket owner wants to grant permission to objects but not all objects are owned by bucket owner, object owner must first grant permission to bucket owner. Done using ACL.
- No. ELs > No. AZs > No. Regions
- Identify inexpensive but slow retrieval sotrage class - **Glacier** (other options 1-Zone-IA, IA, RRS, S3)
- T/F CloudFront origin can be S3/EC2/ELB/Elemental MediaPackage endpoint - **True** - use CustomOriginConfig to specify
- T/F ACLs can be used to make entire buckets public - **True** (also policies, or both)
- Which of these does Transfer Acceleration use to get data into AWS Quicker? **Edge Locations**

Simple questions:
- Characteristics of cloud
- T/F x service is global
- T/F x service is suitable for this e.g. S3 flat file storage
- identify all valid IAM access types
- Best description of a region - physical location with multiple, ioslated, and physically separate AZs within a geographic area
- AZs per region