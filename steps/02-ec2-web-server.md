# EC2 Web Server Setup

## 1. Overview
This step involves provisioning an EC2 instance to host the PrestaShop web application.

---

## 2. Instance Configuration
- Name: prestashop-web-server
- OS: Ubuntu Server 24.04 LTS
- Instance Type: t3.micro (Free Tier eligible)

---

## 3. Key Pair
- Created RSA key pair for secure SSH access
- Private key stored locally and secured

---

## 4. Network and Security
Configured security group rules:

- SSH (22) - Restricted to personal IP
- HTTP (80) - Open to public
- HTTPS (443) - Open to public

This ensures:
- Secure administrative access
- Public accessibility for web application

---

## 5. Storage
- Default 8GB EBS volume used (Free Tier compliant)

---

## 6. Instance Access
- Connected via SSH using private key authentication
- Verified successful access to Ubuntu environment 

---

## 7. Key Observations
- Security groups act as a virtual firewall
- Restricting SSH access reduces attack surface

## Evidence 

**EC2 launch page**

![Launch page](/screenshots/ec2/ec2-launch-page.png)

**Instance running**

![Instance](/screenshots/ec2/instance-running.png)

**Security group rules**

![Rules](/screenshots/ec2/security-group-rules.png)

**SSH terminal connection**

![SSH terminal](/screenshots/ec2/ssh-terminal-connection.png)

---

## Next Step
Provisioning of Amazon RDS MySQL database for application backend.