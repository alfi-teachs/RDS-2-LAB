# RDS-2-LAB

# RDS-LAB-1

# Step 1

Go to AWS Console → EC2 → Launch Instance

Configure:

Name: any (e.g., rds-client)

AMI: Amazon Linux 2

Instance Type: t2.micro

Key Pair: Create and download .pem

Network Settings:

Select your VPC
Select Subnet (AZ)

Security Group (Very Important):
Add inbound rules:

| type        | port         | source  |
|-------------|--------------|---------|
| SSH         | 22           | MY IP   |
| CUSTOM TCP  | 8080         |  Anywhere (0.0.0.0/0) |


Click Launch

# Step 2: Connect to EC2
```bash
ssh -i key.pem ec2-user@<EC2-PUBLIC-IP>
```
  
2. Switch to root user
```bash
sudo su
```
3. Update packages
```bash
yum update -y
```
# Step 3
1. Install Docker
```bash
yum install docker -y
```
2. Start Docker service
```bash
systemctl start docker
```
3. Check Docker status
```bash
systemctl status docker
```
4. Enable Docker on boot (important)
```bash
systemctl enable docker
```
5. Test Docker
```bash
docker run hello-world
```
# Step 4

Steps to Run phpMyAdmin using Docker

1. Pull phpMyAdmin Image from Docker Hub

```bash
docker pull phpmyadmin/phpmyadmin
```

2. Verify Image Downloaded

```bash
docker images
```

4. Run phpMyAdmin Container
   
Usage with arbitrary server

```bash
docker run --name phpmyadmin -d -e PMA_ARBITRARY=1 -p 8080:80 phpmyadmin
```
What this does:

--name phpmyadmin → container name

-d → run in background

-e PMA_ARBITRARY=1 → connect to any MySQL server

-p 8080:80 → access via browser on port 8080

4. Check Running Containers

```bash
docker ps
```
# Step 5

1. Access phpMyAdmin in Browser

```bash
http://<EC2-PUBLIC-IP>:8080
```
# ⚠️ Important

Make sure port 8080 is open in your EC2 Security Group

You need a MySQL server to connect inside phpMyAdmin
--------------------------------------------------------


install PostgreSQL on Amazon Linux 2023

Amazon Linux 2023 uses dnf + PostgreSQL modules, not the old packages.

# 🚀 Step 1: Install PostgreSQL (server + client)
sudo dnf install postgresql15-server -y
# 🚀 Step 2: Initialize database
sudo /usr/bin/postgresql-setup --initdb
# 🚀 Step 3: Start service
sudo systemctl start postgresql
# 🚀 Step 4: Enable on boot
sudo systemctl enable postgresql
# 🚀 Step 5: Switch user
sudo su - postgres
# step 6 :Check client (psql)
psql --version
# step 7 Check PostgreSQL service (server)
systemctl status postgresql
# 🚀 Step 8 : Open PostgreSQL shell
psql

Security Group (very important)

Go to RDS → Security Group:

Add inbound rule:

Type: PostgreSQL
Port: 5432
Source: your EC2 security group



psql -h database-1.c1q0e0awq6n7.ap-south-1.rds.amazonaws.com -U admin -d postgres

Enter password: admin12345


Create database
POSTGRES SQL
Choose a database creation method: Full configuration
Templates: Templates
AZ:Single-AZ DB instance deployment (1 instance)
Settings
DB instance identifier: database-1
Credentials Settings: postgres
Credentials management:Self managed
Master password : admin12345
Confirm master password:admin12345
Additional credentials settings
Password authentication
Instance configuration: 
Burstable classes (includes t classes)
Instance type: dbt4.micro
Storage: General Purpose (gp2)
Allocated storage: 20 GB
Additional storage configuration
Enable storage autoscaling: ✅ Yes
Maximum storage threshold: 1000 GB

Connectivity
Connect to an EC2 compute resource
EC2 instance
DB subnet group
Public access: no 
VPC security group (firewall)

Choose existing
Additional VPC security group: launch wizard4
Availability Zone

Additional Settings
Keep everything default
create database




