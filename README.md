# RDS-2-LAB

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




