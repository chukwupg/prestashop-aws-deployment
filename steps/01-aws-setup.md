# AWS Setup and Environment Configuration

## 1. Overview
This document describes the initial setup of AWS environment used for deploying PrestaShop on a cloud infrastructure using AWS Free Tier.

The objective is to prepare a secure and consistent environment for deployment of both application and database layers.

---

## 2. AWS Account Setup
- Created and logged into AWS Management Console
- Verified account eligibility for AWS Free Tier services

---

## 3. Region Selection
- Selected AWS Region: **us-east-1 (N. Virginia)**
- This region was chosen due to:
  - Full Free Tier support
  - High service availability
  - Standardized documentation and compatibility

---

## 4. Security Configuration
- Enabled Multi-Factor Authentication (MFA) on root account
- Root account access restricted to billing and account-level management
- IAM security best practices observed

---

## 5. Free Tier Verification
- Confirmed eligibility for:
  - Amazon EC2 Free Tier (t2.micro / t3.micro)
  - Amazon RDS Free Tier (MySQL)
- Verified billing dashboard for usage tracking

---

## 6. Design Considerations
- Cloud environment will follow a **two-tier architecture**
  - Web Server (EC2)
  - Database Server (RDS MySQL)
- This separation ensures:
  - Improved security
  - Scalability
  - Best practice cloud architecture

> The database was deployed using Amazon RDS to ensure it is logically and physically separated from the application server, satisfying the requirement that the database must not reside on the same server as the application.

## Evidence

**AWS Management Console with selected region**

![AWS Console](/screenshots/aws-console/created-new-aws-free-tier-account.png)

**Free Tier Dashboard**

![Free tier](/screenshots/aws-console/free-tier-dashboard.png)

**IAM MFA setup page**

![MFA setup](/screenshots/aws-console/mfa-setup.png)

---

## Next Step
Provisioning of EC2 instance for PrestaShop web server setup.