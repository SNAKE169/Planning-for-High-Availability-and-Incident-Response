# Infrastructure

## AWS Zones
us-east-2 ("us-east-2a","us-east-2b","us-east-2c") and us-west-1 ("us-west-1c","us-west-1a")

## Servers and Clusters

### Table 1.1 Summary
| Asset      | Purpose           | Size                                                                   | Qty                                                             | DR                                                                                                           |
|------------|-------------------|------------------------------------------------------------------------|-----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| Asset name | Brief description | AWS size eg. t3.micro (if applicable, not all assets will have a size) | Number of nodes/replicas or just how many of a particular asset | Identify if this asset is deployed to DR, replicated, created in multiple locations or just stored elsewhere |

| VPC | Virtual Private Cloud | N/A | 2 in total, 1 per region | created in multiple locations |
| Internet Gateway | public subnets | N/A | 2 in total, 1 per region | created in multiple locations |
| Private Subnet | not accessible directly from internet | N/A | 1 per availability zone in each region | created in multiple locations |
| Public Subnet | accessible directly from internet | N/A | 1 per availability zone in each region | created in multiple locations |
| NAT Gateway | Network Address Translation | N/A | 1 per availability zone in each region | created in multiple locations |
| EIP | Elastic IP Address | N/A | 1 per availability zone in each region | created in multiple locations |
| ALB | 	Application Load Balancer | N/A | 1 per region | created in multiple locations |
| EC2 | Web server | t3.micro | 3 per region | created in multiple locations |
| EKS | Monitoring | t3.medium | 1 cluster (2 nodes minimum) per region | created in multiple locations |
| RDS | database | db.t2.small	 | 1 cluster (3 instances) per region | Clusters replicated between zones 1 and 2 |

### Descriptions
More detailed descriptions of each asset identified above.
EKS Cluster support Prometheus monitoring and Grafana visualization.
## DR Plan
### Pre-Steps:
List steps you would perform to setup the infrastructure in the other region. It doesn't have to be super detailed, but high-level should suffice.
1. Create ALB in first zone.
2. Increase number of EC2 instance in the first region and route traffic to that ALB.
3. Increase number of RDS, EKS instances.
4. Apply steps above to other regions.

## Steps:
You won't actually perform these steps, but write out what you would do to "fail-over" your application and database cluster to the other region. Think about all the pieces that were setup and how you would use those in the other region
1. Point DNS to the Zone2.
2. Failover RDS cluster.