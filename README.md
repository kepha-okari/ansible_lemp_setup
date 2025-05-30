# Ansible LEMP Stack Provisioning

## 📦 What this project does

This Ansible project provisions a fresh Ubuntu 24.04 droplet with:
- **Nginx**
- **MySQL** (root credentials and `.env` support)
- **PHP** (with FPM)
- **Docker**
- **Python 3**

## 🛠 How to Use

1. Set your droplet's IP in `inventories/production/hosts.ini`
2. Encrypt MySQL password in `group_vars/all/vault.yml`
3. Run the playbook:

```bash
ansible-playbook site.yml
