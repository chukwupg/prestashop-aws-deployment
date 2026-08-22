# RDS MySQL Database Setup

## 1. Overview
This step involves provisioning a managed MySQL database using Amazon RDS to host PrestaShop application data.

---

## 2. Database Configuration
- Engine: MySQL
- Template: Free Tier
- DB Instance Identifier: prestashop-db
- Instance Type: db.t3.micro

---

## 3. Authentication
- Master Username: admin
- Password: [secured and stored safely]

---

## 4. Network Configuration
- Deployed within default VPC
- Public Access: Disabled

This ensures the database is not exposed to the internet.

---

## 5. Security Group Configuration
Created a dedicated security group for database access.

Inbound rule:
- MySQL (3306) - Allowed only from EC2 security group

This enforces:
- Restricted access
- Application-only connectivity

---

## 6. Endpoint Configuration
- RDS endpoint generated for internal communication
- Used later for application database connection

---

## 7. Observations
- RDS provides a managed database environment
- Separation of database and application improves security and scalability


## Evidence 

**RDS creation page**

![RDS created](/screenshots/rds/rds-creation-page.png)

**DB instance details**

![Intance details](/screenshots/rds/db-instance-details.png)

**Security group rule showing EC2 Security Group allowed**

![SG rule](/screenshots/rds/security-group-rule.png)

**Endpoint screen**

![Endpoint](/screenshots/rds/endpoint-screen.png)

---

## Next Step
Installation and configuration of PrestaShop on EC2 and connecting it to RDS database.