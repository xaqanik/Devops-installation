# How to Install Ansible on Debian/Ubuntu

## 1. Update Package Lists

First, update your package lists:

```bash
sudo apt update
```

## 2. Install Ansible

Install Ansible using the following command:

```bash
sudo apt install ansible -y
```

## 3. Verify the Installation

You can verify that Ansible has been installed correctly by checking its version:

```bash
ansible --version
```

## 4. Create an Inventory File (Optional)

Ansible uses an inventory file to manage hosts. You can create a simple inventory file at `/etc/ansible/hosts`:

```bash
[servers]
server1 ansible_host=203.0.113.10
server2 ansible_host=203.0.113.11
```

You can then ping all the servers in your inventory:

```bash
ansible -i /etc/ansible/hosts all -m ping
```
