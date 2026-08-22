# PrestaShop Deployment on AWS EC2 with External RDS Database

## 1. Overview

This stage covers the deployment of PrestaShop (an open-source e-commerce platform) on an AWS EC2 instance, integrated with a separate AWS RDS MySQL database instance. The architecture follows a two-tier design model to ensure separation of application and database layers.

---

## 2. Architecture Summary

- **Application Layer:** AWS EC2 (Ubuntu Server + Apache + PHP)
- **Database Layer:** AWS RDS (MySQL)
- **Access Layer:** Public EC2 IP (HTTP)

This ensures that the database is not hosted on the same server as the application, in compliance with the project requirements.

---

## 3. EC2 Web Server Setup

The EC2 instance was configured as follows:

- Updated system packages
- Installed Apache web server
- Installed PHP and required extensions for PrestaShop compatibility

### Installed Components:
- apache2
- php
- php-mysql
- php-curl
- php-gd
- php-intl
- php-mbstring
- php-xml
- php-zip

Apache service was enabled and started to serve web traffic.

---

## 4. PrestaShop Installation

PrestaShop was downloaded and deployed into the Apache web root directory.

### Steps:

- Navigated to web root:
```
cd /var/www/html
```

- Downloaded PrestaShop package:
```
wget https://github.com/PrestaShop/PrestaShop/releases/download/8.1.2/prestashop_8.1.2.zip
```

- Extracted application files:
```
sudo unzip prestashop_8.1.2.zip
```

- Cleaned up installation archive:
```
rm prestashop_8.1.2.zip
```

## 5. File Permissions Configuration

Correct permissions were applied to ensure Apache could serve the application:

```
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html
```

---

## 6. PrestaShop Web Installer Configuration

The installation wizard was accessed via the EC2 public IP

`http://98.91.188.49`

### Database Settings Used:

- Database Server: RDS Endpoint
- Database Name: prestashop_db
- Username: admin
- Password: (configured RDS password)

## 7. Issues Encountered and Resolutions

### 7.1 Dynamic Public IP Change (EC2 Restart)

During deployment, the EC2 instance public IP changed after a stop/start operation. This caused SSH access interruption due to IP-restricted security group rules.

Resolution:

- Updated AWS Security Group inbound rule to allow SSH from the new client IP
- Continued deployment without rebuilding infrastructure

### 8.2 PrestaShop Compatibility Errors

During Prestashop setup, missing dependencies were detected:

- Apache mod_rewrite not enabled
- PHP intl extension missing

#### Resolution:

- Enabled apache mod_rewrite
```
sudo a2enmod rewrite
```
- Installed missing dependencies 
```
sudo apt install php-intl -y
```
- Restarted Apache
```
sudo systemctl restart apache2
```

### 8.4 Database Not Found Error

After configuring prestashop to use RDS endpoint as the database server, and suuplying the credentials needed to connect to it, PrestaShop connected successfully but reported missing database.

#### Resolution:

- Created database directly on RDS via EC2 MySQL client

```
sudo apt update
sudo apt install mysql-client -y

mysql -h <RDS-ENDPOINT> -u admin -p
```

#### Database Creation:

```SQL
CREATE DATABASE prestashop_db;
EXIT; 
```

- Ensured correct database name (prestashop_db) was used


## 10. Outcome
- PrestaShop successfully deployed on EC2
- External RDS database successfully integrated
- Application is accessible via public EC2 IP
- Two-tier cloud architecture successfully implemented

## Evidence

**Apache test page**

![Apache test page](/screenshots/working-app/apache-test-page.png)

**PrestaShop installer screen**

![Installer screen](/screenshots/working-app/prestashop-installation.png)

**DB connection screen**

![DB connection](/screenshots/working-app/db-connection-screen.png)

**Final working homepage**

![Final working homepage](/screenshots/working-app/final-working-homepage.png)

## 11. Next Step

Proceeding to security hardening and necessary deployment optimization.