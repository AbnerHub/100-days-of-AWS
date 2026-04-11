## Day 37: Managing EC2 Access with S3 Role-based Permissions

The Nautilus DevOps team needs to set up an application on an EC2 instance to interact with an S3 bucket for storing and retrieving data.
To achieve this, the team must create a private S3 bucket, set appropriate IAM policies and roles, and test the application functionality.

Task:

1) EC2 Instance Setup:
   
- An instance named `nautilus-ec2` already exists.
- The instance requires access to an S3 bucket.

2) Setup SSH Keys:

- Create new SSH key pair (id_rsa and id_rsa.pub) on the `aws-client` host and add the public key to the `root` user's authorized keys on the EC2 instance.

3) Create a Private S3 Bucket:

- Name the bucket `nautilus-s3-821328497772.`
- Ensure the bucket is private.

4) Create an IAM Policy and Role:

- Create an IAM policy allowing `s3:PutObject`, `s3:ListBucket` and `s3:GetObject` access to `nautilus-s3-821328497772.`
- Create an IAM role named `nautilus-role.`
- Attach the policy to the IAM role.
- Attach this role to the `nautilus-ec2` instance.
  
5) Test the Access:

- SSH into the EC2 instance and try to upload a file to `nautilus-s3-821328497772`.

## Setup SSH Keys

```
ssh-keygen -t rsa
```
```
cat /root/.ssh/id_rsa.pub
```

```
sudo su ~
vi /root/.ssh/authorized_keys
```

```
ssh -i id_rsa root@public-ec2-ip 
```


## Create a Private S3 Bucket

<img width="1280" height="629" alt="image" src="https://github.com/user-attachments/assets/a6ab2370-58c7-4fbb-b9f4-ea587dac109c" />

<img width="1496" height="572" alt="image" src="https://github.com/user-attachments/assets/1e89daee-0142-4ac8-aef7-f0a7afac9513" />

## Create an IAM Policy and Role

<img width="1244" height="673" alt="image" src="https://github.com/user-attachments/assets/a248f3a7-31e7-4a83-a08c-03b209519b87" />

## EC2 Instance Setup

<img width="1522" height="340" alt="image" src="https://github.com/user-attachments/assets/fef1cb2d-6dd4-4532-9b76-157c3d30f73b" />



<img width="1235" height="676" alt="image" src="https://github.com/user-attachments/assets/38e1b8d5-ac72-43b6-bfac-5deb4ffec6d4" />


## Test the Access

```
vi s3test.txt
```

bucket using following command:

```
aws s3 cp <your-file> s3://nautilus-s3-821328497772/
```

- Now run following command to list the upload file:
  
```
aws s3 ls s3://nautilus-s3-821328497772/
```
