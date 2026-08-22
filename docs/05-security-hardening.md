# Security Hardening

## 1. Overview

After successful deployment of PrestaShop on AWS EC2 with an external RDS database, I performed security hardening to reduce the attack surface and enforce best practices across system, application, and network layers.

---

## 2. EC2 Hardening (OS & SSH)

### Disable SSH Password Authentication

```
sudo nano /etc/ssh/sshd_config
```
Set:
```
PasswordAuthentication no
PermitRootLogin no
```
Restart SSH:
```
sudo systemctl restart ssh
```

### Purpose:

Prevents brute-force attacks by enforcing key-based authentication only.

### Evidence

**EC2 SSH hardening (Password Authentication and Port)**

![EC2 hardening](/screenshots/security-hardening/ec2-ssh-hardening.png)

---

## 2. Configure Firewall (UFW)
Configured Uncomplicated firewall to only allow the specified connections
```
sudo apt install ufw -y
sudo ufw allow 2002
sudo ufw allow 80
sudo ufw enable
sudo ufw status
```

### Purpose:

Restricts incoming traffic to only required services (SSH and HTTP).

### Evidence

**Uncomplicated firewall configuration**

![UFW](/screenshots/security-hardening/enable-firewall-ufw.png)

---

## 3. Apache Hardening

### Disable Directory Listing
```
sudo nano /etc/apache2/apache2.conf
```
Change:
```
Options Indexes FollowSymLinks
```
To:
```
Options FollowSymLinks
```
Restart Apache:
```
sudo systemctl restart apache2
```

### Purpose:
Prevents attackers from viewing directory contents.

### Hide Apache Version Information
```
sudo nano /etc/apache2/conf-available/security.conf
```
Set:
```
ServerTokens Prod
ServerSignature Off
```
Restart:
```
sudo systemctl restart apache2
```

### Purpose:
Reduces information disclosure that could aid attackers.

### Evidence

**Disable Directory listing**

![Disable directory listing](/screenshots/security-hardening/apache-hardening-disable-directory-listing.png)

**Hide Apache Version information**

![Hide version info](/screenshots/security-hardening/apache-hardening-hide-version-info.png)

---

## 4. RDS Hardening

### Restrict Database Access 

To only allow connection comming from the EC2 instance

- **Port:** 3306
- **Source:** EC2 Security Group ONLY`

Removed:

`0.0.0.0/0`

### Purpose:
Ensures only the application server can communicate with the database.

### Disable Public Access

Set RDS instance to:

**Public Access:** NO

### Purpose:

Prevents direct internet exposure of the database.

### Evidence

**RDS Security Group**

![RDS security group](/screenshots/security-hardening/rds-hardening-security-group.png)

**RDS Disabled gateway access**

![RDS no public access](/screenshots/security-hardening/rds-hardening-disabled-public-access.png)

---

## 5. AWS Security Group Hardening

EC2 Security Group Rules

| Port | Purpose | Source     |
| ---- | ------- | ---------- |
| 2002   | SSH     | My IP only |
| 80   | HTTP    | 0.0.0.0/0  |


### Actions Taken:

- Restricted SSH to a single trusted IP
- Removed unnecessary open ports

### Evidence

**Security Group Rules**

![SG Rules](/screenshots/security-hardening/security-group-hardening.png)

---

## 6. Application-Level Hardening (PrestaShop)

### Remove Installation Directory
```
sudo rm -rf /var/www/html/install
```

### Purpose:
Prevents reinstallation attacks.

### Secure Admin Directory
```
cd /var/www/html
ls
sudo mv admin* admin_secure
```

### Purpose:
Obfuscates admin access path to reduce brute-force attempts.

### Evidence

**Removed Prestashop installation directory**

![Delete installer](/screenshots/security-hardening/prestashop-hardening-delete-installer.png)

**Renamed Admin directory**

![Renamed Admin directory](/screenshots/security-hardening/prestashop-hardening-rename-admin-directory.png)

---

## 7. Configure File Permissions

Applied secure permissions to enforce principle of least privilege.

```
sudo find /var/www/html -type f -exec chmod 644 {} \;
sudo find /var/www/html -type d -exec chmod 755 {} \;
```
### Permission Breakdown
**File Permission: 644**
- **Owner:** Read, Write
- **Group:** Read
- **Others:** Read

#### Security Impact:

- Files are readable by the web server
- Prevents unauthorized modification or execution

**Directory Permission: 755**
- **Owner:** Read, Write, Execute
- **Group:** Read, Execute
- **Others:** Read, Execute

#### Security Impact:

- Allows directory traversal by Apache
- Prevents unauthorized write access

### Evidence

**File and directory permissions**

![Permissions](/screenshots/security-hardening/prestashop-hardening-set-file-and-directory-permissions.png)

---

## 8. Security Summary

The system was successfully hardened across:

- Operating System (SSH restrictions, firewall)
- Web Server (Apache configuration)
- Database Layer (RDS isolation and access control)
- Application Layer (PrestaShop security measures)
- File System (Permission enforcement)

This multi-layered approach ensures reduced exposure to common attack vectors such as brute-force attacks, unauthorized access, and information disclosure.

---