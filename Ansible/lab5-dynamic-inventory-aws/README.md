# 🧠 Lab 5: Automated Host Discovery with Ansible Dynamic Inventory

This project demonstrates how to automatically discover and manage AWS EC2 instances using **Ansible Dynamic Inventory**.

---

## 🚀 Objectives
- Create an AWS EC2 instance with a specific tag (`ivolve`).
- Configure Ansible Dynamic Inventory using the `aws_ec2` plugin.
- Automatically discover and list running EC2 instances.
- Verify the setup using Ansible ad-hoc commands and playbooks.

---

## 🛠️ Steps Overview

### 1. Create EC2 Instance
Created an EC2 instance on AWS and assigned the tag:
- **Name:** ivolve

### 2. Configure Dynamic Inventory
Created an inventory file named **my_inventory.aws_ec2.yml**:

```yaml
plugin: aws_ec2
regions:
  - eu-central-1
keyed_groups:
  - key: tags.Name
filters:
  tag:Name: ivolve
```
### 3. List Target Hosts

- **Command:**
```
ansible-inventory -i my_inventory.aws_ec2.yml --graph
```

Output confirms Ansible detected the tagged instance.

### 4. Verify Connection

- **Command:**
```
ansible all -m ping
```

- **Response:**
```
pong
```
### 5. Run a Test Playbook

- **Executed:**
```
ansible-playbook -i my_inventory.aws_ec2.yml test.yml
```

- **Sample test.yml:**

---
```
- name: Test connection and print message
  hosts: all
  tasks:
    - name: Print Hello message
      debug:
        msg: "Hello from Ansible to AWS EC2!"
```
