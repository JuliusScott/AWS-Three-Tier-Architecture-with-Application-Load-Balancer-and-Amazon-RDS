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

## Skills Demonstrated

Designed, deployed, and troubleshot AWS infrastructure while applying cloud networking, high availability, load balancing, database connectivity, cloud security, Linux administration, and AWS CLI skills aligned with CompTIA Cloud+, Network+, Security+, LPI Linux Essentials, and AWS Solutions Architect Associate concepts.

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
