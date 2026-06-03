## Phase 1 - Create VPC
1.	Configure VPC settings within the AWS Console.
2.	Create a VPC name that identifies the lab.
3.	Configure:
o	2 Public Subnets
o	2 Private Application Subnets
o	2 Private Database Subnets
4.	Select NAT Gateway (Regional).
o	Required for private EC2 instances to download packages and updates.
5.	Review and create the VPC.

## Phase 2 Create Security Groups
### 1.	Application Load Balancer –
o	Allows inbound HTTP 80 from 0.0.0.0 
o	Allows outbound HTTP 80 to the EC2 security group.

### 2.	EC2 Instance
o	Allows inbound HTTP 80 from the ALB security group. 
o	Allows outbound HTTPS 443 for updates and Systems Manager.
o	Allow outbound MySQL 3306 to RDS 

### 3.	Endpoints 
o	Allows inbound HTTPS 443 from the EC2 security group. 

### 4.	AWS RDS
o	Allows inbound MySQL 3306 from the EC2 security group.

## Phase 3 - Create an IAM role.
1.	Create and configure a role.
2.	Trusted Entity
o	AWS service
o	EC2 Role for AWS Systems Manager – 
3.	attaches AmazonSSMManagedInstanceCore.
4.	Create role

## Phase 4 Build Infrastructure
### Create VPC Endpoints
AWS Services
o	SSM
o	SSMMessages
o	EC2Messages

1.	Place each endpoint into two private subnets.
2.	One subnet per availability zone.
3.	Attach the Endpoints security group to each service.

### Create Application Load Balancer
1.	Create ALB
2.	Select Internet-facing
3.	Select two public subnets
4.	Attach ALB Security Group
Screenshot Validation

### Create Target Group
1.	Target Type = Instance
2.	Protocol = HTTP
3.	Port = 80
4.	Select VPC

### Launch EC2 Instances
1.	Launch EC2 Instance AZ1
2.	Launch EC2 Instance AZ2
3.	Place instances into private application subnets
4.	Attach EC2 Security Group
5.	Attach SSM IAM Role
6.	Add User Data Script

### Register Targets
1.	Register both EC2 instances with the Target Group

### Create RDS Subnet Group
1.	Select two private database subnets
2.	One subnet per Availability Zone

### Create RDS Database
Engine:
•	MySQL

Configuration:
•	Dev/Test
•	Single-AZ Deployment
•	Self-Managed Credentials
•	db.t3.micro
•	20 GB Storage

Networking:
•	VPC
•	RDS Subnet Group
•	RDS Security Group

Connectivity:
•	Connect to EC2 Instance


## Phase 5 - Validation
Application Load Balancer
ALB DNS loads webpage
Target Group healthy

Systems Manager
EC2 appears in Fleet Manager
Session Manager connection successful

EC2 Validation
Apache installed
Apache running
curl http://localhost successful

RDS Validation
EC2 connects to MySQL
Database created
