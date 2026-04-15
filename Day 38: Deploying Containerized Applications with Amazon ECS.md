## 📌 Overview

The Nautilus DevOps team is tasked with deploying a containerized application using Amazon's container services. 
They need to create a private Amazon Elastic Container Registry (ECR) to store their Docker images and use Amazon Elastic Container Service (ECS) to deploy the application. 
The process involves building a Docker image from a given Dockerfile, pushing it to the ECR, and then setting up an ECS cluster to run the application.

**1.Create a Private ECR Repository:**
  - Create a private ECR repository named `devops-ecr` to store Docker images.

**2.Build and Push Docker Image:**
  - Use the Dockerfile located at `/root/pyapp` on the `aws-client` host.
  - Build a Docker image using this Dockerfile.
  - Tag the image with latest tag.
  - Push the Docker image to the `devops-ecr` repository.

**3.Create and Configure ECS cluster:**

  - Create an ECS cluster named `devops-cluster` using the Fargate launch type.

**4.Create an ECS Task Definition:**

  - Define a task named `devops-taskdefinition` using the Docker image from the `devops-ecr` ECR repository.
  - Specify necessary CPU and memory resources.

**5.Deploy the Application Using ECS Service:**

  - Create a service named `devops-service` on the `devops-cluster` to run the task.
  - Ensure the service runs at least one task.


## 🚀 1. Crearing repo in AWS console

1. Open Amazon ECR
2. Create Repository / Private Repository
3. Write your respository name `devops-ecr`
5. For image tag muable
   - Mutable:
6. Encryptation config
   - AES-256

<img width="882" height="620" alt="repo" src="https://github.com/user-attachments/assets/80952ced-102a-4724-967e-889db54b6e9b" />

## 2.Build and Push Docker Image:

Access to your directory where is located the Docker file:

```
cd /root/pyapp
```

On `aws-client`, build an image and give it a name "devops-image", it could be whatever you want. 

```
docker build -t devops-image .
```

**Authenticate your Docker client to AWS ECR**

```bash
aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.<region>.amazonaws.com
```

My authentication:

```bash
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 692377628692.dkr.ecr.us-east-1.amazonaws.com/devops-ecr
```

**Tag your image**

```bash
docker tag <image-id> <aws_account_id>.dkr.ecr.<region>.amazonaws.com/<my-repository-name>:<tag>
```
to know your image-id, run:
```
docker images
```

<img width="722" height="100" alt="image" src="https://github.com/user-attachments/assets/5083a6a7-a95e-47f0-871d-a7dcfa48810a" />

my tag: 
```bash
docker tag 48a76e77b72d 692377628692.dkr.ecr.us-east-1.amazonaws.com/devops-ecr:latest
```

**note:** devops-ecr its the same ECR name repository created in AWS, both names should match.


**Push the image**
```bash
docker push <aws_account_id>.dkr.ecr.<region>.amazonaws.com/<my-repository>:<tag>
```
Example:
```bash
docker push 692377628692.dkr.ecr.us-east-1.amazonaws.com/devops-ecr:latest
```

## 3. Create and Configure ECS cluster:

1) Access to AWS ECS servoce and click on clusters on the dashboard navigation panel.

<img width="905" height="311" alt="image" src="https://github.com/user-attachments/assets/81768f0f-8978-460d-ad4e-c81435243a91" />

2) Create a new cluster, naming it `devops-cluster` 

<img width="905" height="358" alt="image" src="https://github.com/user-attachments/assets/6037a463-1b01-473c-9c4e-d9b675ec401e" />


## 4.Create an ECS Task Definition:

1) On the dasbboard navigation panel, click on task definition to create one.

<img width="1064" height="311" alt="image" src="https://github.com/user-attachments/assets/e9a99a89-6cad-434f-bda0-458033b99821" />


2) Click on create a new task definition and name it as `devops-taskdefinition`

3) On infraestructure requirements secction:
   - Launch type: Fargate
   -  Operating Sistem: Linux/x86_64
   -  CPU: 3
   -  Memory: 3GB
    
<img width="1035" height="690" alt="image" src="https://github.com/user-attachments/assets/9e0b9c00-ccdc-432f-9ceb-4f8c1544f233" />


4) On Container-1 secction
   
   - Name: devops-ecs-1
   - Image URI:Browse ECR images and select `devops-ecr`
   
   <img width="1267" height="480" alt="image" src="https://github.com/user-attachments/assets/ed36ebad-939a-4599-9b7a-5eabaa56f4bb" />

5) Leave the other options as default and click on create.


## 5. Deploy the Application Using ECS Service

Create a service named `devops-service` on the `devops-cluster` to run a task.
 1. Go to Cluster on te ECS dashboard navigation
 2. On the `Service` tab, click on create 

<img width="1476" height="346" alt="image" src="https://github.com/user-attachments/assets/81bb20aa-9880-4872-8126-37cfa69a721a" />

3. On the service details secction, select `devops-taskdefinition` and write the service name `devops-service`

4. On the environment panel, select **Fargate** as Launch type. 

<img width="1048" height="752" alt="image" src="https://github.com/user-attachments/assets/b64f6379-e9c5-4492-93f8-ca39283db8d6" />


## Test the environment 

1) On VPC service go to Security Groups and modify default security group, adding http and 0.0.0.0/0 source.

<img width="1798" height="505" alt="image" src="https://github.com/user-attachments/assets/4313b050-48f1-4576-acf0-0f4893fecd6e" />


2) From ECS Dashboard, go to `Clusters >  devops-cluster > tasks` and copy the public-clip

3) On a browser, paste the ip copied, and you´ll see `Welcom to KKE AWS Cloud Labs!` message






