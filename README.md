# AWS Three-Tier Architecture with Application Load Balancer and Amazon RDS

## Project Overview

This project demonstrates the deployment of a highly available three-tier web application architecture on AWS. The environment uses a custom VPC with public and private subnets across multiple Availability Zones. An Application Load Balancer distributes traffic to EC2 web servers hosted in private subnets, while Amazon RDS MySQL provides the database tier.

## Architecture Components

- Amazon VPC
- Public and Private Subnets
- Internet Gateway
- NAT Gateway
- Application Load Balancer
- Amazon EC2
- Amazon RDS MySQL
- Security Groups
- Route Tables
- AWS Systems Manager Session Manager

## Skills Demonstrated

- AWS Networking
- High Availability Design
- Load Balancing
- Database Connectivity
- Cloud Security
- Linux Administration
- AWS CLI
- Troubleshooting

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
