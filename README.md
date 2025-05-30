# Ansible LEMP Stack Provisioning

## Project Overview

This Ansible project automates the provisioning of a production-ready LEMP stack (Linux, Nginx, MySQL, PHP) on a fresh Ubuntu 24.04 server. It also installs Docker and Python 3, making it suitable for modern web application deployments.

**Features:**
- Installs and configures Nginx as a web server
- Installs MySQL with secure root credentials (supports .env integration)
- Installs PHP with FPM and common extensions
- Installs Docker for containerized workloads
- Installs Python 3 for scripting and automation
- Uses Ansible best practices: roles, variables, and vault for secrets

---

## Prerequisites

- **Ansible** (v2.10+ recommended)
- **SSH access** to your Ubuntu 24.04 server
- **Python 3** installed on your local machine
- **Vault password file** for encrypted secrets (see below)

---

## Inventory & Variables

1. **Set your server IP:**
   - Edit `inventories/production/hosts.ini` and add your droplet/server IP under the `[lemp]` group.

2. **Configure secrets:**
   - Edit `group_vars/all/vault.yml` to set your MySQL root password and any other sensitive variables.
   - Use Ansible Vault to encrypt this file:
     ```bash
     ansible-vault encrypt group_vars/all/vault.yml --vault-password-file vault-pass.txt
     ```
   - Example variables:
     ```yaml
     mysql_root_password: your_strong_password
     ```

---

## Playbook Structure

- `site.yml` — Main playbook entry point
- `roles/` — Contains modular roles:
  - `nginx/` — Installs and configures Nginx
  - `mysql/` — Installs and secures MySQL
  - `php/` — Installs PHP and extensions
  - `docker/` — Installs Docker
  - `python/` — Installs Python 3
- `group_vars/all/vault.yml` — Encrypted secrets
- `inventories/production/hosts.ini` — Inventory file

---

## How to Use

1. **Set your droplet's IP in** `inventories/production/hosts.ini`
2. **Encrypt MySQL password in** `group_vars/all/vault.yml`
3. **Run the playbook:**
   ```bash
   ansible-playbook -i inventories/production/hosts.ini site.yml --vault-password-file vault-pass.txt
   ```

---

## Customization

- **Add PHP extensions:**
  - Edit `roles/php/tasks/main.yml` to include additional PHP packages.
- **Customize Nginx config:**
  - Modify `roles/nginx/tasks/main.yml` or add templates for your site.
- **Add more roles:**
  - Create new roles in `roles/` and include them in `site.yml` as needed.

---

## Troubleshooting & FAQ

- **Q: Playbook fails on SSH connection?**
  - A: Ensure your SSH key is added to the server and your user has sudo privileges.
- **Q: Vault decryption error?**
  - A: Make sure you use the correct `vault-pass.txt` file and that `vault.yml` is encrypted.
- **Q: How do I reset MySQL root password?**
  - A: Update the password in `vault.yml`, re-encrypt, and re-run the playbook.

---

## License

MIT License. See `LICENSE` file for details.
