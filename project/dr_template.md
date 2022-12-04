# Infrastructure

## AWS Zones

Identify your zones here
Region :us-east-2, AZS: us-east-2a, us-east-2b,us-east-2c
Region :us-west-1, AZS: us-west-1b, us-west-1c

## Servers and Clusters

### Table 1.1 Summary

| Asset                   | Purpose                                       | Size                                                                   | Qty                                                             | DR                                                                                                           |
| ----------------------- | --------------------------------------------- | ---------------------------------------------------------------------- | --------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| Asset name              | Brief description                             | AWS size eg. t3.micro (if applicable, not all assets will have a size) | Number of nodes/replicas or just how many of a particular asset | Identify if this asset is deployed to DR, replicated, created in multiple locations or just stored elsewhere |
| EC2 instances/webserver | Ubuntu webserver                              | t3.micro                                                               | 3                                                               | yes                                                                                                          |
| EKS instance            | eks cluster for grafana/prometheus monitoring | t3.medium                                                              | 2                                                               | yes                                                                                                          |
| RDS primary instance    | mysql aurora DB instance                      | db.t2.small                                                            | 2 instance in each region. replicated in other region           | yes (data is replicated to secondary instance)                                                               |
| Load balancer           | load balancer for webserver                   | -                                                                      | -                                                               | yes                                                                                                          |
| VPC                     | network configuration of ec2 cluster          | -                                                                      | each region has its own network or vpc setup                    | yes                                                                                                          |

### Descriptions

EC2 webserver instances host apis
EKS instances - host grafana/prometheus stack for monitoring
RDS instances - mysql aurora database to store data
LBS intances -> load balance the request in each region
VPC instances -> virtual private network setup for AWS EC2 instance.

## DR Plan

### Pre-Steps:

Deploy assets in multiple region
Create a cloud load balancer and point DNS to the load balancer and it help us to have multiple instances behind 1 IP in a region
Have a replicated database

## Steps:

Configure DNS entry at your DNS provider to point to the DR site.
As we have already setup database replication,configure DR database cluster as active in real time.
