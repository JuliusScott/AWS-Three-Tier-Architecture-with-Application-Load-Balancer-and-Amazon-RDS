# Notes and Lessons Learned

## Overview

This document contains troubleshooting notes, lessons learned, and validation steps encountered while building the AWS Three-Tier Architecture project. The environment was deployed using private application and database tiers, an Application Load Balancer (ALB), Amazon RDS MySQL, and AWS Systems Manager Session Manager for secure administration.

---

# AWS Systems Manager Session Manager

## Purpose

AWS Systems Manager Session Manager was used to securely access EC2 instances deployed in private subnets without opening inbound SSH ports or assigning public IP addresses.

## Benefits

Session Manager provided:

* Secure shell access to EC2 instances.
* No requirement for public IP addresses.
* No requirement for inbound SSH access.
* Encrypted communication between AWS and EC2 instances.
* Centralized administration through AWS Systems Manager.
* Reduced attack surface by eliminating publicly exposed management ports.

## Validation Activities

Session Manager was used throughout the project to:

* Verify Apache installation.
* Confirm user-data execution.
* Validate hostname configuration.
* Check web server status.
* Test package installation.
* Verify network connectivity.
* Connect to Amazon RDS MySQL.
* Troubleshoot application deployment issues.

Example commands executed through Session Manager:

```bash
systemctl status httpd

hostname -f

mysql --version

mysql -h <rds-endpoint> -u admin -p
```

## Result

Successfully administered private EC2 instances without exposing SSH ports to the public internet, demonstrating a secure alternative to traditional remote administration methods.

---

# Issue 1: EC2 Instances Unable to Install Packages

## Problem

EC2 instances deployed in private subnets were unable to install Apache (httpd), PHP, and MariaDB client packages during initialization.

## Cause

The private subnets did not initially have outbound internet connectivity.

Without outbound internet access, package repositories could not be reached.

## Resolution

Created a NAT Gateway within a public subnet and updated the private route tables to send internet-bound traffic through the NAT Gateway.

## Result

EC2 instances successfully downloaded and installed required packages through user-data scripts.

---

# Issue 2: Session Manager Could Not Connect to EC2 Instances

## Problem

Systems Manager initially could not establish sessions with private EC2 instances.

## Cause

The required Systems Manager communication path was incomplete.

## Resolution

Configured the necessary AWS Systems Manager VPC Endpoints:

* SSM
* EC2Messages
* SSMMessages

Verified that the EC2 instances were registered as managed nodes.

## Result

Successfully connected to private EC2 instances through Session Manager without requiring SSH access.

---

# Issue 3: Application Load Balancer Health Checks Failed

## Problem

The Application Load Balancer initially reported unhealthy targets.

## Cause

Health checks were unable to successfully validate the web application.

## Resolution

* Verified Apache was running.
* Confirmed security group communication between ALB and EC2.
* Reviewed target group health check configuration.
* Tested web content locally from the EC2 instances.

## Result

Targets became healthy and traffic was successfully distributed across both application servers.

---

# Issue 4: Validating Load Balancer Traffic Distribution

## Problem

Needed to verify that the Application Load Balancer was routing requests to multiple EC2 instances.

## Resolution

Configured the web page to display the hostname of each EC2 instance:

```html
<h1>You did it Julius! King of the clouds $(hostname -f)</h1>
```

Refreshing the ALB DNS endpoint displayed different EC2 hostnames from separate Availability Zones.

## Result

Confirmed successful traffic distribution across multiple EC2 instances.

---

# Issue 5: Amazon RDS Connectivity Validation

## Problem

Needed to verify communication between the application and database tiers.

## Resolution

Connected to EC2 instances using Session Manager and tested database connectivity using:

```bash
mysql -h <rds-endpoint> -u admin -p
```

Verified:

* Database connectivity
* Network communication
* Security group configuration
* DNS resolution

## Result

Successfully established communication between EC2 and Amazon RDS MySQL.

---

# Issue 6: Security Group Design

## Problem

Needed to implement secure communication between application components while minimizing exposure.

## Resolution

Configured least-privilege access:

* Internet → ALB (HTTP)
* ALB → EC2 (HTTP)
* EC2 → RDS (MySQL 3306)

Administrative access was performed through AWS Systems Manager Session Manager rather than opening inbound SSH ports.

## Result

Application functionality was maintained while reducing unnecessary network exposure.

---

# Key Takeaways

* AWS Systems Manager Session Manager enables secure administration without exposing SSH to the internet.
* NAT Gateways are required when private resources need outbound internet access.
* Load Balancer health checks are critical for application availability.
* Security groups should be configured using least-privilege principles.
* Hostname-based validation is an effective way to verify load balancing functionality.
* End-to-end testing should be performed after every major deployment milestone.
* Troubleshooting cloud infrastructure improves understanding of AWS service dependencies and networking concepts.
