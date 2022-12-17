# Infrastructure

## AWS Zones
us-east-2 ("us-east-2a","us-east-2b","us-east-2c") and us-west-1 ("us-west-1c","us-west-1a")

## Servers and Clusters

### Table 1.1 Summary
| Asset      | Purpose           | Size                                                                   | Qty                                                             | DR                                                                                                           |
|------------|-------------------|------------------------------------------------------------------------|-----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| Asset name | Brief description | AWS size eg. t3.micro (if applicable, not all assets will have a size) | Number of nodes/replicas or just how many of a particular asset | Identify if this asset is deployed to DR, replicated, created in multiple locations or just stored elsewhere |

| VM | running application | t3.medium | 3 instances | is deployed to DR |
 |EKS | monitoring stack | t3.medium | 2 nodes (EKS) | is deployed to DR |
| VPC | virtual private cloud |  | | has IPs in multiple availability zones|
| ALB | application load balancer |  | #number of region | created in each region |
|SQL cluster | storing data |  | 2 clusters, 2 instances/ each cluster| is created in multiple locations |

### Descriptions
More detailed descriptions of each asset identified above.
For SQL cluster, set the backup retention window to 5 days. Each cluster must have multiple availability zones. Zone1 will replicate to a cluster in zone2
## DR Plan
### Pre-Steps:
List steps you would perform to setup the infrastructure in the other region. It doesn't have to be super detailed, but high-level should suffice.
1. Ensure the infrastructure is set up and working in the DR site.
2. Double-check infrastructure comply with the design.

## Steps:
You won't actually perform these steps, but write out what you would do to "fail-over" your application and database cluster to the other region. Think about all the pieces that were setup and how you would use those in the other region
1. Point DNS to the load balancer. This way you can have multiple instances behind 1 IP in a region. During a failover scenario, you would fail over the single DNS entry at your DNS provider to point to the DR site. This is much more intelligent than pointing to a single instance of a web server.