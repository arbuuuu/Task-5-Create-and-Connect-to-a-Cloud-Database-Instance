# Task-5-Create-and-Connect-to-a-Cloud-Database-Instance
To understand how **Cloud Databases** work by creating a **managed SQL database instance** (like MySQL or PostgreSQL) in the cloud, connecting to it, and performing basic CRUD operations.

# ☁️ Task 5: Create and Connect to a Cloud Database Instance

## 🎯 Objective

To understand how **Cloud Databases** work by creating a **managed SQL database instance** (like MySQL or PostgreSQL) in the cloud, connecting to it, and performing basic CRUD operations.

---

## 🛠️ Tools Used

- **AWS RDS (Free Tier)** — for hosting the MySQL database
- **MySQL Workbench / DBeaver / VS Code Terminal** — for connection
- **Python (mysql.connector)** — for remote data access

---

## 📋 Steps Performed

### 1️⃣ Create a Cloud Database Instance
- Logged into AWS Management Console.
- Navigated to **RDS → Create Database → MySQL**.
- Selected free-tier configuration.
- Created a DB instance with:
  - Region: Asia Pacific (Mumbai)
  - Username: `admin`
  - Password: `********`
- Waited for provisioning to complete.

### 2️⃣ Configure Access
- Enabled **Public access**.
- Added my system IP under **VPC security group inbound rules**.
- Noted the **Endpoint (host)** for connection.

### 3️⃣ Connect to Database
Used **MySQL Workbench**:

Host: your-db-endpoint.rds.amazonaws.com
Port: 3306
Username: admin
Password: yourpassword


Connection was successful ✅

---

## 🧱 SQL Setup

### Create Database and Table
```sql
CREATE DATABASE intern_demo;
USE intern_demo;

CREATE TABLE students (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(50),
  domain VARCHAR(30),
  score INT
);

Insert Sample Data:
INSERT INTO students (name, domain, score)
VALUES ('Aarav', 'Cloud', 95),
       ('Diya', 'DevOps', 89);

View Data:
SELECT * FROM students;

Python Connection Script:
import mysql.connector

conn = mysql.connector.connect(
  host="your-cloud-sql-ip",
  user="root",
  password="yourpassword",
  database="intern_demo"
)

cursor = conn.cursor()
cursor.execute("SELECT * FROM students")

for row in cursor.fetchall():
    print(row)

conn.close()


