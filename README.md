# 🚀 Ansible EC2 Automation Project (AWS)

This project automates AWS EC2 lifecycle operations using Ansible:
- Create EC2 instances
- Terminate EC2 instances
  
 =============================================================
<h1>NOTE</h1>
==============================================================
🐍 Python Virtual Environment (venv)
📌 Why we use venv in this project

This project uses a Python virtual environment (venv) to keep all dependencies isolated and avoid conflicts with system-wide Python packages.

🧠 Problem without venv

If we install packages globally in the system:

Different projects can use different package versions
System Python can get corrupted
Tools like Ansible may fail due to missing or incompatible dependencies
Installation requires admin/sudo access

This leads to unstable and hard-to-debug environments.


✅ Solution: Virtual Environment

A virtual environment creates a separate isolated workspace for Python dependencies.

Each project gets its own:

Python packages
Package versions
Execution environment

============================================================================================================================================================================

---

# 📌 Tech Stack
- Ansible
- AWS EC2
- boto3 / botocore
- Python (venv recommended)
- WSL / Linux environment

- # 📁 Project Structure

Ansible_EC2_task/
│
├── ec2_create.yml
├── ec2_stop.yml
├── ec2_terminate.yml
│
├── group_vars/
│ └── all/
│ ├── aws_secrets.yml
│ └── aws_secrets.yml.example
│
├── inventory.ini (optional)
├── .gitignore
└── README.md


---

# ⚙️ Prerequisites

## Install WSL (Windows)
```powershell```
wsl --install

Install Python + venv
sudo apt update
sudo apt install python3 python3-venv -y


Create Virtual Environment
python3 -m venv venv
source venv/bin/activate

Install required libraries
pip install boto3 botocore ansible


Setup Vault
 openssl rand -base64 2048 > vault.pass

 Add aws credentail to vault
   ansible-vault edit group_vars/all/pass.yml --vault-password-file vault.pass

🔐 AWS Credentials Setup
Create file:
  group_vars/all/aws_secrets.yml
  Example:
aws_access_key: YOUR_ACCESS_KEY
aws_secret_key: YOUR_SECRET_KEY

🚀 How to Run (WSL / Linux)
  1️⃣ Create EC2 Instances
  ansible-playbook ec2_create.yml --vault-password-file vault.pass

  3️⃣ Terminate EC2 Instances (⚠️ Permanent Delete)
  ansible-playbook ec2_terminate.yml --vault-password-file vault.pass

  🪟 Windows (PowerShell) Usage
      If using WSL from Windows:
        wsl
cd ~/projects/Ansible_EC2_task
source venv/bin/activate
ansible-playbook ec2_create.yml --vault-password-file vault.pass


⚠️ Important Notes
DO NOT upload:
vault.pass
.pem files
real AWS credentials
Always use .gitignore
    
