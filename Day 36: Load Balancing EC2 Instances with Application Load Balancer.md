## 📌 Overview

The Nautilus Development Team needs to set up a new EC2 instance and configure it to run a web server. 
This EC2 instance should be part of an Application Load Balancer (ALB) setup to ensure high availability and better traffic management. 
The task involves creating an EC2 instance, setting up an ALB, configuring a target group, and ensuring the web server is accessible via the ALB DNS.

**Create a security group:**
Create a security group named `nautilus-sg` to open port `80` for the `default` security group (which will be attached to the ALB). 
Attach nautilus-sg security group to the EC2 instance.

**Create an EC2 instance:** 
Create an EC2 instance named `nautilus-ec2.` 
Use any available Ubuntu AMI to create this instance. Configure the instance to run a user data script during its launch.

This script should:

- Install the Nginx package.
- Start the Nginx service.

**Set up an Application Load Balancer:**
Set up an Application Load Balancer named `nautilus-alb.` Attach `default` security group to the same.

**Create a target group:** 
Create a target group named `nautilus-tg.`

**Route traffic:** 
The ALB should route traffic on port `80` to port `80`of the `nautilus-ec2` instance.

**Security group adjustments:**
Make appropriate changes in the ``default`` security group attached to the ALB if necessary. Eventually, the Nginx server running under ``nautilus-ec2`` 
instance must be accessible using the ALB DNS.

## 🚀 Create a instance sg

<img width="1520" height="697" alt="image" src="https://github.com/user-attachments/assets/e2a14a30-e04e-4f95-83b7-c0fa3e29e5ef" />

## Create an EC2 instance

<img width="975" height="656" alt="image" src="https://github.com/user-attachments/assets/abf65f99-9558-4078-a446-9669e4bb6324" />


<img width="1500" height="449" alt="image" src="https://github.com/user-attachments/assets/49046dfc-0ccf-40a4-aec2-d585512cc79b" />


```
#!/bin/bash

# 1. Update the local package index
echo "Updating system packages..."
sudo apt update -y

# 2. Install Nginx
echo "Installing Nginx..."
sudo apt install nginx -y

# 3. Start Nginx service
echo "Starting Nginx..."
sudo systemctl start nginx

# 4. Enable Nginx to start on boot
sudo systemctl enable nginx
```

## Create a target group

<img width="1213" height="789" alt="image" src="https://github.com/user-attachments/assets/f46f38bb-33c9-43ae-8ce5-81a73415d01b" />


<img width="1257" height="669" alt="image" src="https://github.com/user-attachments/assets/c30c1c2e-8f3e-46b4-b9b6-291651f6b48f" />


<img width="1621" height="759" alt="image" src="https://github.com/user-attachments/assets/36280267-75ef-4edf-b306-12c9fe1a2080" />

## Set up an Application Load Balancer

<img width="1060" height="578" alt="image" src="https://github.com/user-attachments/assets/34b3759e-f675-45a8-a3db-ddc5b9f779ae" />

<img width="1329" height="634" alt="image" src="https://github.com/user-attachments/assets/1418653d-af36-49de-ae4e-be40f33b3b9e" />

<img width="1333" height="618" alt="image" src="https://github.com/user-attachments/assets/d255170d-8d94-411a-9821-c40a09f92c5f" />


## Security group adjustments

<img width="1608" height="478" alt="image" src="https://github.com/user-attachments/assets/f367c1a1-581e-4327-b400-fdc7588a0526" />

