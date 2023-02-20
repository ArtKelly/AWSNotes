ub# Elastic Block store 
Storage volumes for EC2


- Production Workloads
- Highly Available
	- Automatically replicated within a single availability zone to protect against hardware failures
- Scalable
	- Dynamically increase capacity and change the volume type with no downtime or performance impact

### General Purpose SSD (gp2)
- 3 IOPS per GiB, up to a max 16,000 IOPS per volume
- gp2 volumes smaller than 1TB
- Good for boot volumes or development and test applications 

### gp3
- Predictable 3,000 IOPS baseline performance
- Ideal for applications that require high performance at a low cost, such as MySQL, Cassandra, virtual desktops, and Hadoop analytics.
- Customers looks for higher performance can scale up to 16,000 IOPS and 1,000 MiB/s for an additional fee

### Provisioned IOPS SSD (io1)
- 64,000 IOPS per volume, 50 IOPS per GiB
- Use if you need more than 16,000 IOPS.

### io2
- Same price as io2
- 64,000 IOPS, 500 IOPS/GiB
- 99.999% durability
- I/O intensive apps, large databases, and latency-sensitive workloads

### Throughput Optimized HDD (st1)
- Baseline 40MB/s per TB
- Ability to burst upto 250MB/s per TB
- Maximum throughput of 500MB/s per volume
- Frequently accessed, throughput sensitive workloads
- Big-data, data warehouses, ETL, and log processing
- A cost effective way to store lots of data
- Cannot be a boot drive

### Cold HDD (sc1)
Lowest cost option
- Baseline throughput of 12MB/s per TB
- Ability to burst up to 80MB/s per TB
- Max throughput of 250 MB/s per volume
- A good choice for colder data requiring fewer scans per day
- Good for applications that need the lowest cost and performance is not a factor

### IOPS vs Throughput
- IOPS Measures the number of read and write operations per second
- Important metric for quick transactions
- The ability to action reads and writes very quickly 
- Choose provisioned IOPS SSD (io1, io2)
- Throughput measures the number of bits read or written per second
- Important metric for large datasets, large I/O sizes, Complex queries
- The ability to deal with large datasets
- Choose Throughput Optimized HDD (st1)

## Volumes and Snapshots
 - Volumes exist on EBS
 - Virtual HDD
	 - You need a minimum of 1 volume per EC2 instance
- Snapshots exist on S3
	- A snapshot of the virtual disk/volume
	- Point in time copy of a volume
	- Snapshots are incremental
		- Only the changed data since your last snapshot is backed up to s3
	- The first snapshot takes longer than subsequent snapshots
- Consitant snapshots
	- Snapshots only contain data that has been written to your EBS volume
	- Stop the EC2 before snapshot
- Encrypted Snapshot
	- If you snapshot of an encrypted EBS volume, the snapshot will be encrypted automatically
- Sharing Snapshots
	- You can only share snapshots in the region they were created. Otherwise you need to copy them to the destination region.
- EBS Volumes will always be in the same AZ as your EC2

### EBS Encryption
