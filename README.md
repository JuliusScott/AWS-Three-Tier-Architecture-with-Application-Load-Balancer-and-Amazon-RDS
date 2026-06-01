# AWS Three-Tier Architecture with Application Load Balancer and Amazon RDS

## Project Overview

This project demonstrates the deployment of a highly available three-tier web application architecture on AWS. The environment uses a custom VPC with public and private subnets across multiple Availability Zones. An Application Load Balancer distributes traffic to EC2 web servers hosted in private subnets, while Amazon RDS MySQL provides the database tier.

## Architecture Components

## Architecture Components

| Networking | Compute & Services |
|------------|-------------------|
| Amazon VPC | Amazon EC2 |
| Public and Private Subnets | Application Load Balancer |
| Internet Gateway | Amazon RDS MySQL |
| NAT Gateway | AWS Systems Manager Session Manager |
| Route Tables | Security Groups |

## Skills Demonstrated

- Designed and configured AWS networking components, including VPCs, subnets, route tables, and gateways.
- Implemented a highly available architecture across multiple Availability Zones.
- Configured an Application Load Balancer to distribute traffic across multiple EC2 instances.
- Established secure connectivity between the application and database tiers using Amazon RDS MySQL.
- Applied cloud security best practices through the use of security groups and least-privilege access.
- Utilized Linux administration skills to configure and manage EC2 instances.
- Deployed and managed AWS resources using the AWS Command Line Interface (CLI).
- Validated system functionality and resolved infrastructure issues through troubleshooting and testing.

## Certification Alignment

- CompTIA Cloud+
- CompTIA Network+
- CompTIA Security+
- LPI Linux Essentials
- AWS Solutions Architect Associate

## Repository Structure

```text
architecture/   - Architecture diagrams
screenshots/    - Validation and deployment screenshots
scripts/        - AWS CLI commands and Bash scripts
notes/          - Troubleshooting notes and lessons learned
