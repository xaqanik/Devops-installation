# How to Install Terraform on Debian/Ubuntu

## 1. Install Required Packages

First, update your package lists and install the necessary packages:

```bash
sudo apt update
sudo apt install -y gnupg software-properties-common curl
```

## 2. Add the HashiCorp GPG Key

Add the HashiCorp GPG key:

```bash
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
```

## 3. Add the Terraform Repository

Add the official HashiCorp Linux repository:

```bash
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
```

## 4. Install Terraform

Update your package lists and install Terraform:

```bash
sudo apt update
sudo apt install terraform -y
```

## 5. Verify the Installation

Verify that Terraform is installed correctly by checking its version:

```bash
terraform --version
```
