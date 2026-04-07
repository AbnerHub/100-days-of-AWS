# 📌 Day 35: Deploying and Managing Applications on AWS

The Nautilus DevOps team needs a new private RDS instance for their application. They need to set up a MySQL database and ensure that their existing EC2 instance can connect to it. This will help in managing their database needs efficiently and securely.

1) Task Details:

    - Create a private `RDS instance` named `nautilus-rds` using a `sandbox` template.
    - The engine type must be `MySQL v8.4.5`, and it must be a `db.t3.micro` type instance.
    - The **master username** must be `nautilus_admin` with an appropriate password.
    - The **RDS storage** type must be `gp2`, and the storage size must be `5GiB`.
    - **Create a database** named `nautilus_db`.
    - Keep the rest of the configurations as default. Ensure the instance is in `available` state.
    - **Adjust the security groups** so that the `nautilus-ec2` instance can connect to the RDS on port `3306` and also open port `80` for the instance.

2) An EC2 instance named `nautilus-ec2` exists. Connect to this instance from the AWS console. Create an `SSH` key (`/root/.ssh/id_rsa`) on the `aws-client` host if it doesn't already exist. Add the public key to the `authorized_keys` of the root user on the EC2 instance for password-less SSH access.

3) There is a file named `index.php` under the `/root` directory on the `aws-client` host. Copy this file to the `nautilus-ec2` instance under the `/var/www/html/` directory. Make the appropriate changes in the file to connect to the RDS.

4) You should see a `Connected successfully` message in the browser once you access the instance using the **public IP**.

## 🚀 Creating a RDS instance
1) Sign in with the credentials given to AWS console and open RDS service, then click on create database
2) - in engine option choose `MySQL`
   - database cretion method choose `full configuration`
   - templates `free Tier`
   <img width="800" height="400" alt="rds1" src="https://github.com/user-attachments/assets/6dcbaa36-13d2-4e21-906a-f7531adc8ee6" />

3) Create the database with the names given in the instructions (Admin,RDS unstance name and creatre a password)
<img width="800" height="600" alt="password-rds" src="https://github.com/user-attachments/assets/f33e15f2-03a4-47a1-8607-e7a18997ecf8" />
      
4) Create  a database  `nautilus_db`
   <img width="800" height="400" alt="db-rds" src="https://github.com/user-attachments/assets/78bd217d-d418-42e8-8e6c-fed4842f56f0" />

6)  On connectivity seccion
   - on `compute resource` choose dont connect to an EC2 compute resource
   - `vpc` default
   - `security group` create a new decurity group

     <img width="800" height="600" alt="rds-sg" src="https://github.com/user-attachments/assets/22f8becf-d0f3-4c83-a1e7-8e8e92aaf06c" />

7) Once created and launched the rds instance, check its `endpoint`, we´ll use it later.
<img width="800" height="600" alt="endpoint" src="https://github.com/user-attachments/assets/324bb88c-1453-4935-bd56-931e8eef9898" />
   
## Set up firewalles rules
1) EC2 istance has a defautlt sg, delete it and create a new one: `ec2-instance-sg`
    > inbound rules
     - http port 80 **source** 0.0.0.0/0
     - ssh por 22 **source** 0.0.0.0/0 
    > outbound rules
    - all traffic source 0.0.0.0/0
2) Set up RDS sg created before. adding a new inbound rule
   - MYSQL/Aurora port  3306 **Source** ec2-instance-sg
     
## Connect to ec2 instance from aws-client 
## Adjust index.php file
## Verify connection 



