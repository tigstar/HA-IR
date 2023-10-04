# Infrastructure

## AWS Zones
us-east-2 : us-east-2a, us-east-2b, us-east-2c
us-west-1 : us-west-1b, us-west-1c

## Servers and Clusters

### Table 1.1 Summary
| Asset | Purpose | Size | Qty | DR |
|-------|---------|------|-----|----|
| EC2 | Hosting a business application | t3.micro | 2 | Created in us-east-2 |
| EC2 | Hosting a business application | t3.micro | 2 | Replica in us-west-1 |
| EKS | For monitoring stack | t3.medium | 2 nodes cluster | Created in us-east-2 |
| EKS | For monitoring stack | t3.medium | 2 nodes cluster | Replica in us-west-1 |
| VPC | Virtual private network | 3 subnets | 1 | Created in different availability zones us-east-2a, us-east-2b, us-east-2c |
| VPC | Virtual private network | 2 subnets | 1 | Created in different availability zones us-west-1a, us-west-1b |
| ALB | Application Load balancer for the business application | N/A | 1 | Created in us-east-2 |
| ALB | Application Load balancer for the business application | N/A | 1 |Created in us-west-1 |
| RDS | Backend database  | db.t3.micro | 2 nodes cluster | Created in us-east-2 |
| RDS | Backend database  | db.t3.micro | 2 nodes cluster | Replica in us-west-1 |
| GitHub | Terraform Code | ~  50 KB | 1 | GitHub |

### Descriptions
* EC2 : Three EC2 instances in each region (us-east-2 and us-west-1) across three Availability Zones. This ensures that your web application is highly available and can continue to operate even if one Availability Zone goes down.
* EKS An EKS cluster in each region, used to deploy and manage the monitoring platform.
* VPC: A VPC in each region, with three IP addresses in us-east-2 and two IP addresses in us-west-1 in each Availability Zone. This provides networking for the EC2 instances and the EKS cluster.
* ALB: An ALB in each region, used to distribute incoming traffic across the EC2 instances.
* RDS: A primary RDS cluster in us-east-2 and a secondary RDS cluster in us-west-1, configured for geo-replication. This ensures that the database is highly available and can continue to operate even if one region goes down.
* Github : for storing terraform code which is an infrastructure as code tool that allows you to define your infrastructure in a human-readable configuration file. This makes it easy to deploy and manage your infrastructure in a consistent and repeatable way.

## DR Plan
### Pre-Steps:
1. The SRE engineer has access to AWS DR resources.
2. Verify that the DR is ready, set up and working.
## Steps:

1. Use load balancer with a single DNS record to distribute traffic across multiple web servers in a region. During a failover, switch the DNS record to point to the DR site.

2. Use replica database and fail over to the DR instance during a disaster. This is faster than restoring from backup. Ideally, the application should use a generic DNS record to connect to the database, so it can automatically connect to the DR instance after a failover.