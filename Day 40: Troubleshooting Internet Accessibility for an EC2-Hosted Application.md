## 📌 Task review

The Nautilus Development Team recently deployed a new web application hosted on an EC2 instance within a public VPC named `xfusion-vpc`.
The application, running on an Nginx server, should be accessible from the internet on port 80. 
Despite configuring the security group `xfusion-sg` to allow traffic on port 80 and verifying the EC2 instance settings, 
the application remains inaccessible from the internet. The team suspects that the issue might be related to the VPC configuration, 
as all other components appear to be set up correctly. The DevOps team has been asked to troubleshoot and resolve the issue to ensure 
the application is accessible to external users.

As a member of the Nautilus DevOps Team, your task is to perform the following:

**1. Verify VPC Configuration:**
Ensure that the VPC `xfusion-vpc` is properly configured to allow internet access.

**2. Ensure Accessibility:**
Make sure the EC2 instance `xfusion-ec2` running the Nginx server is accessible from the internet on port 80.


## 🚀  Verify VPC Configuration:

Access to VPC service on you AWS console.
1. In the  dashboard navigation panel select VPC´s
2. Choose `xfusion-vpc`
3. Select resource map
     
Here we  notice that there is not an internet gateway connected to our vpc so, there is not Internet access


<img width="1498" height="596" alt="image" src="https://github.com/user-attachments/assets/04732378-407d-42d0-a14f-2ead8e6a8320" />


In the services path into VPC service

1. Go to Internet Gateways
2. Select `xfusion-ig` an attach it to `xfusion-vpc`

<img width="1431" height="286" alt="image" src="https://github.com/user-attachments/assets/f814d29d-228a-440c-94a3-d309a62c593d" />


Paste the public ip of your `xfusion-ec2` instance iin a browser. You will see `Welcome to nginx!` message. 
