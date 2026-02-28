# Data Migration From EC2 to RDS

## :round_pushpin: Introduction
Database migration is the process of transferring data from one database environment to another. In this practical, we performed the migration of a MariaDB 105 database from an Amazon EC2 instance to Amazon RDS. The objective was to move from a self-managed database setup to a fully managed database service provided by AWS. This migration improves scalability, security, backup management, and maintenance. The process involved creating a database backup using mysqldump and importing it securely into the RDS instance using SSL connectivity.

##  :construction: Architecture Diagram

![Reference Image](/img/Architecture.png)

## :bulb: Implementation Steps.
### Step 1: Create RDS Database.
- Full configuration
- Select Mariadb105
- Database Name
- Master Username (admin)
- Self managed
- Auto generated password
- Create Database

![Reference Image](/img/img1.png)

### Step 2: Launch Instance
- Name (Traditional-DB)
- Select AMI
- Key pair
- Security Group
- Launch instance
  
![Reference Image](/img/img2.png)

### Step 3: Install Mariadb105-server
  ```bash
  sudo yum update
  sudo yum install mariadb105-server
  sudo systemctl start mariadb
  sudo systemctl enable mariadb
  sudo systemctl status mariadb
  ```

![Reference Image](/img/img3.png)

### Step 4: Create database student_db

![Reference Image](/img/img4.png)

### Step 5: Insert student data in table
- Show databases
- Use (database name)
- Insert into student values
- Select * from (table name)

![Reference Image](/img/img5.png)

### Step 6: Create SQL file
- mysqldump -u root -p student_db > student_bkp. sql

![Reference Image](/img/img6.png)

### Step 7: Access the RDS Database & Create database student_DB

![Reference Image](/img/img7.png)

### Step 8: Extract file into RDS server and display student data on the RDS Database.
- mysq1 -h migrate-database. c6ti0au6uj68. us-east-1. rds. amazonaws. com -u admin -p -- ssl student_DB < student_bkp. sql
- Show databases
- use (database name)
- show tables
- select * from (table name)

![Reference Image](/img/img8.png)

## 📌 Summary
This practical demonstrates the migration of a MariaDB 105 database from an EC2 instance to Amazon RDS. A backup of the source database (student-db) was created using the mysqldump utility, generating the student_bkp.sql file. The backup file was then securely transferred and imported into the Amazon RDS MariaDB instance using an SSL connection. Data migrate EC2 to RDS.
