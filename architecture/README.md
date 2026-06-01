# Architecture Diagram

This diagram illustrates the AWS Three-Tier Architecture deployed in this project.

## Components

- Amazon VPC
- Internet Gateway
- Public Subnets
- Private Application Subnets
- Private Database Subnets
- Application Load Balancer (ALB)
- Amazon EC2
- Amazon RDS MySQL
- Security Groups
- Route Tables

## Traffic Flow

Internet → Application Load Balancer → EC2 Application Tier → Amazon RDS Database Tier

## Availability

The environment spans two Availability Zones to improve fault tolerance and availability.

## Security

Application servers and database resources are deployed in private subnets. AWS Systems Manager Session Manager is used for administrative access without exposing SSH to the public internet.
