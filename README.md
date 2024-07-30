Ansible Playbook for Automated Deployment and Configuration
This repository contains an Ansible playbook to automate the deployment and configuration of a boilerplate application on an AWS EC2 instance.

Prerequisites
An AWS EC2 instance running Ubuntu 22.04.
Ansible installed on your local machine or control node.
SSH access to your EC2 instance.
Files
main.yaml: Ansible playbook for deploying and configuring the application.
inventory.cfg: Ansible inventory file listing the target server.
Setup
Step 1: Clone the Repository
Clone this repository to your local machine or control node:

bash
Copy code
git clone https://github.com/your_username/your_repository.git
cd your_repository
Step 2: Update Inventory File
Edit the inventory.cfg file to include your EC2 instance's public DNS or IP address:

ini
Copy code
[hng]
ec2-xx-xx-xx-xx.compute.amazonaws.com ansible_ssh_private_key_file=/path/to/your/keypair.pem ansible_user=ubuntu
Step 3: Run the Ansible Playbook
Execute the playbook to deploy and configure your application:

bash
Copy code
ansible-playbook main.yaml -i inventory.cfg -b
Main Tasks
1. Clone Repository into /opt Directory
The playbook clones the specified repository into the /opt/stage_5b directory and sets the correct permissions.

2. Install Dependencies
The playbook installs all required dependencies for the application, including PostgreSQL and any messaging queues like RabbitMQ or Redis.

3. Configure PostgreSQL
The playbook configures a PostgreSQL database and saves the admin credentials in /var/secrets/pg_pw.txt.

4. Setup Nginx
The playbook sets up Nginx to reverse proxy requests from port 80 to the application running on port 3000.

5. Logging
The playbook configures logging so that stderr logs are written to /var/log/stage_5b/error.log and stdout logs to /var/log/stage_5b/out.log, both owned by the hng user.
