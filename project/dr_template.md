# Infrastructure

## AWS Zones

Identify your zones here
us-east-2a, us-east-2b

## Servers and Clusters

### Table 1.1 Summary

| Asset        | Purpose                     | Size                                                                   | Qty                                                             | DR                                                                                                           |
| ------------ | --------------------------- | ---------------------------------------------------------------------- | --------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| Asset name   | Brief description           | AWS size eg. t3.micro (if applicable, not all assets will have a size) | Number of nodes/replicas or just how many of a particular asset | Identify if this asset is deployed to DR, replicated, created in multiple locations or just stored elsewhere |
| EC2 Instance | Deploy flask application    | t3.micro                                                               | 3                                                               | DR                                                                                                           |
| EKS          | Host Prometheus and Grafana | t3.medium                                                              | 2                                                               | DR                                                                                                           |
| ALB          | Domain for Grafana          |                                                                        | 1                                                               | DR                                                                                                           |
| RDS          | Replication Demo            | t2.small                                                               | 2                                                               | Replicated                                                                                                   |

### Descriptions

More detailed descriptions of each asset identified above.

- EC2 Instance: The EC2 Instance is used to host the Flask web application. A node exporter is installed inside instances to export metrics to Prometheus.
- EKS: A Kubernetes cluster is spinned up to deploy Prometheus and Grafana.
- ALB: The ALB acts like an internet-facing mask and used as a domain for Grafana.
- RDS: The RDS is used mainly to demonstrate data replication between regions.

## DR Plan

### Pre-Steps:

List steps you would perform to setup the infrastructure in the other region. It doesn't have to be super detailed, but high-level should suffice.

- Ensure both sites are configured the same.
- Use Terraform to deploy infrastructure to each region.

## Steps:

You won't actually perform these steps, but write out what you would do to "fail-over" your application and database cluster to the other region. Think about all the pieces that were setup and how you would use those in the other region

- Point your DNS to your secondary region
  - This can be done with a name provider like Amazon route 53
- Failover your database replication instances to another region
  - Manually force the secondary region to become primary at the database level, or
  - Automatically failover the database by health checks