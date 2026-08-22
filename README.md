# PrestaShop Deployment on AWS (Using EC2 and RDS)

## Project Overview

This project demonstrates the deployment of a PrestaShop e-commerce application on AWS using a secure and scalable architecture.

The setup follows a **two-tier architecture**, separating the application and database layers to meet best practices and design requirements.

---

## Architecture

- **EC2 (Ubuntu):**  Hosts PrestaShop (Apache + PHP)
- **RDS (MySQL):** Hosts database
- **Security Groups:** Control network access
- **Public Access:** Via EC2 public IP

<!--- See: /architecture/architecture-diagram.png -->

---

## 🌍 Live Application

http://98.91.188.49

---

## Implementation Steps

1. Provisioned EC2 instance (Ubuntu)
2. Installed Apache, PHP, and required extensions
3. Configured RDS MySQL database (separate from EC2)
4. Connected EC2 to RDS securely
5. Installed and configured PrestaShop
6. Resolved deployment issues (dependencies, DB config, IP changes)
7. Performed system and application security hardening

---

## Security Highlights

- SSH access restricted to trusted IP
- Disabled password-based SSH login
- Apache hardened (no directory listing, hidden server info)
- RDS access limited to EC2 only
- Removed PrestaShop install directory
- Applied least-privilege file permissions

---

## Challenges & Resolutions

| Challenge | Resolution |
|----------|-----------|
| EC2 IP change | Updated security group rules |
| Missing Apache/PHP modules | Installed required dependencies |
| Database not found | Created DB on RDS and corrected config |
| Installer errors | Enabled mod_rewrite and PHP intl |

---

## Documentation

- AWS Setup: [docs/01-aws-setup.md](docs/01-aws-setup.md)
- EC2 Setup: [docs/02-ec2-web-server.md](docs/02-ec2-web-server.md)
- RDS Setup: [docs/03-rds-database.md](docs/03-rds-database.md)
- PrestaShop Install: [docs/04-prestashop-installation.md](docs/04-prestashop-installation.md)
- Security Hardening: [docs/05-security-hardening.md](docs/05-security-hardening.md)

---

## Outcome

- Fully functional PrestaShop deployment
- External database architecture (EC2 + RDS)
- Secure and hardened environment
- Publicly accessible application

---

## Future Improvements

- Enable HTTPS (SSL/TLS)
- Add AWS WAF
- Configure monitoring (CloudWatch)
- Automate deployment (Terraform/Ansible)

---

## Author

👩‍💻 **Chukwu PraiseGod**  
Follow my journey: [X](https://x.com/chukwupg) | [LinkedIn](https://linkedin.com/in/chukwupg)  