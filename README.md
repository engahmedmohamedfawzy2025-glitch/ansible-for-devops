# Ansible for DevOps Engineers – Practical Learning Guide

> **Goal:** Learn Ansible from scratch as a DevOps Engineer — from setup to integration with Jenkins, GitHub, and AWS — and document your learning for professional visibility.

---

## 🎯 Objectives

You’ll learn how to:
- Understand what Ansible is and why DevOps engineers use it.  
- Set up the Ansible environment.  
- Write and run Playbooks.  
- Manage configurations and automate deployments.  
- Integrate Ansible with Jenkins, GitHub, and AWS.

---

## 📘 Part 1 – Introduction to Ansible

### 🔹 What is Ansible?

**Ansible** is an open-source **Automation & Configuration Management** tool from Red Hat.  
It allows you to:
- Manage thousands of servers from one place.  
- Automate application deployments and configuration changes.  
- Ensure all systems remain consistent and up to date.

---

### 🔹 Why Use Ansible?

| Reason | Description |
|--------|--------------|
| **Agentless** | No agent needs to be installed on managed servers (unlike Puppet or Chef). |
| **Simple Syntax** | Uses YAML, which is human-readable and easy to maintain. |
| **Idempotent** | Running the same playbook multiple times won’t cause repeated changes. |
| **Integration Ready** | Easily integrates with Jenkins, GitHub, Docker, and AWS. |

---

## ⚙️ Part 2 – Core Components of Ansible

| Component | Description |
|------------|-------------|
| **Inventory** | A file that lists all servers (targets) managed by Ansible. |
| **Modules** | Built-in commands that perform specific actions (install, copy, etc.). |
| **Tasks** | Steps that define what actions to perform. |
| **Playbook** | A YAML file describing automation instructions. |
| **Roles** | A structured way to organize and reuse playbooks. |
| **Variables** | Dynamic values to make playbooks flexible. |
| **Handlers** | Tasks triggered only after a change occurs (e.g., restart service). |

---

## 🧰 Part 3 – Lab Setup

### Requirements
- A machine with **Python** and **Ansible** installed.  
- SSH access to target servers.

### Installation (Ubuntu)
```bash
sudo apt update
sudo apt install ansible -y

# Verify installation
ansible --version
Example Inventory File
ini
Copy code
[webservers]
192.168.1.10
192.168.1.11

[dbservers]
192.168.1.20
🧩 Part 4 – Your First Playbook 🎬
File: install-nginx.yml

yaml
Copy code
---
- name: Install and start Nginx
  hosts: webservers
  become: yes

  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present
        update_cache: yes

    - name: Start Nginx service
      service:
        name: nginx
        state: started
        enabled: yes
Run:

bash
Copy code
ansible-playbook -i inventory install-nginx.yml
🧮 Part 5 – Variables & Templates
Variables
yaml
Copy code
---
- hosts: webservers
  vars:
    package_name: nginx
  tasks:
    - name: Install package
      apt:
        name: "{{ package_name }}"
        state: present
Templates (Jinja2)
Template file: index.html.j2

html
Copy code
<html>
  <h1>Welcome to {{ ansible_hostname }}</h1>
</html>
Playbook:

yaml
Copy code
- hosts: webservers
  tasks:
    - name: Copy custom HTML
      template:
        src: index.html.j2
        dest: /var/www/html/index.html
🔁 Part 6 – Role Structure
Example project organization:

bash
Copy code
my-ansible-role/
├── roles/
│   └── nginx/
│       ├── tasks/main.yml
│       ├── templates/index.html.j2
│       └── vars/main.yml
├── inventory
└── site.yml
🔒 Part 7 – Ansible Vault (Secrets Management)
Create an encrypted file:

bash
Copy code
ansible-vault create secrets.yml
Use it in your playbook:

yaml
Copy code
vars_files:
  - secrets.yml
Run the playbook:

bash
Copy code
ansible-playbook site.yml --ask-vault-pass
☁️ Part 8 – Integrations (Jenkins, GitHub, AWS)
Jenkins: Run Ansible playbooks within CI/CD pipelines.

GitHub Actions: Automate environment setup or configuration checks.

AWS EC2: Provision and configure cloud instances automatically.

🧾 Part 9 – Real-World Use Cases
✅ Web application deployment
✅ Server patching and updates
✅ Docker container management
✅ Nginx + SSL configuration

🧠 Part 10 – Professional Tips
Use roles for reusable structure.

Use tags to run specific tasks selectively.

Use --check mode to preview changes before applying them.

Document every playbook clearly.

Integrate Ansible into CI/CD for consistent deployments.

✅ Summary
Ansible is a key DevOps tool for automating, configuring, and orchestrating infrastructure at scale.
It’s simple, powerful, and perfect for ensuring consistency across environments.
