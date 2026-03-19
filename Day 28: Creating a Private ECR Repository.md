# Day 28: Creating a Private ECR Repository

## 📌 Overview
They need to create a private Amazon Elastic Container Registry (ECR) repository to store their Docker images. Once the repository is created, they will build a Docker image from a Dockerfile located on the aws-client host and push this image to the ECR repository. This process is essential for maintaining and deploying containerized applications in a streamlined manner.

Create a private ECR repository named *devops-ecr*. There is a Dockerfile under /root/pyapp directory on aws-client host, build a docker image using this Dockerfile and push the same to the newly created ECR repo, the image tag must be *latest*.

## 🚀 Crearing repo in AWS console

1. Open Amazon ECR
2. Create Repository / Private Repository
3. Write your respository name `devops-ecr`
5. For image tag muable
   - Mutable:
6. Encryptation config
   - AES-256

<img width="1682" height="820" alt="repo" src="https://github.com/user-attachments/assets/80952ced-102a-4724-967e-889db54b6e9b" />

## Build docker image with dockerfile 

On your client, naviate to *pyapp* directory and build your image with: 

```bash
docker build -t python-image .
```

<img width="987" height="663" alt="image" src="https://github.com/user-attachments/assets/475ee3d3-5d11-4d29-a4ff-530fd3f8977d" />

**Authenticate your Docker client to the Amazon ECR**
```bash
aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.<region>.amazonaws.com
```
My authentication:
```bash
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 541882316995.dkr.ecr.us-east-1.amazonaws.com
```

**Tag your image with the Amazon ECR**
```bash
docker tag e9ae3c220b23 aws_account_id.dkr.ecr.region.amazonaws.com/my-repository:tag
```
my tag: 
```bash
docker tag de46d81fbd0f 541882316995.dkr.ecr.us-east-1.amazonaws.com/devops-ecr:latest
```

**note:** devops-ecr its the same ECR name repository created in AWS, both names should match.


**Push the image**
```bash
docker push aws_account_id.dkr.ecr.region.amazonaws.com/my-repository:tag
```
Example:
```bash
docker push 541882316995.dkr.ecr.us-east-1.amazonaws.com/devops-ecr:latest
```
