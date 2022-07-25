↼ [[Index]]

# EC2
## Fundamental service of AWS
- Secure, resizable compute capacity in the cloud
- Pay for what you use
- No wasted capacity
	- Grow and shrink capacity
- Provision in minutes not months

### Pricing
- On demand
- Reserved
	- Most cost efficient
- Spot
	- Price fluctuates with demand
- Dedicated
	- More expensive

####  On demand
- Low cost and flexibility of Amazon EC2
- Short term, spiky or unpredictable workloads that cannot be interrupted
- Testing the water. Applications being developed or tested

#### Reserved instances
- Predictable usage
- Specific capacity requirements
- Pay up front
- Standard RIs
	- Up to 72% off the on-demand price
- Convertible RIs
	- Up to 54% off the on-demand price
		- Has the option to change to a different RI of equal or greater value
- Scheduled RIs
	- Launch within the time window you define
	- Match your capacity reservation to a predictable recurring schedule that only requires a fraction of a day, week or month

#### Spot 
- Specify price to have spot instance.
	- Flexible start and end times
- Good for cost sensitive applications
- Users with an urgent need for additional computing capacity
- Image rendering
- Genomic sequencing
- Algorithmic trading engine

#### Dedicated Hosts
- Compliance
	- Regulatory requirements that may not support multi-tenant virtualisation
- On-demand
	- Can be purchased on demand (hourly)
- Licensing
	- Great for licensing that does not support multi-tenancy or cloud deployments
- Reserved
	- Can be purchased as a reservation for up to 70% off the on-demand price

### CLI
- interact with aws using the command line
- User groups for security

### Using Roles
- Preferred from a security perspective
- Avoid hard coding credentials
- Policies control a roles permissions
- You can update a policy and it will take immediate effect
- You can attach and detach roles to running ec2 instances 

### Security groups and bootstrap scripts
- Virtual firewalls for your EC2 instance. 
	- by default all inbound traffic is blocked
- To let everything in: 0.0.0.0/0
- Bootstrap script runs when the instance first runs
- You can have any number of EC2 instances within a security group
- You can have multiple security groups attached to an EC2
- By default all outbound traffic is allowed

