## 📌 Day 39: Hosting a Static Website on AWS S3

The Nautilus DevOps team has been tasked with creating an internal information portal for public access. 
As part of this project, they need to host a static website on AWS using an S3 bucket. 
The S3 bucket must be configured for public access to allow external users to access the static website directly via the S3 website URL.

**Task Requirements:**

1.Create an S3 bucket named `xfusion-web-22236`.
2.Configure the S3 bucket for static website hosting with `index.html` as the index document.
3.Allow public access to the bucket so that the website is publicly accessible.
4.Upload the `index.html` file from the `/root/` directory of the AWS client host to the S3 bucket.
5.Verify that the website is accessible directly through the S3 website URL.


## 🚀 Create an S3 bucket named `xfusion-web-22236`.

<img width="1340" height="678" alt="image" src="https://github.com/user-attachments/assets/bce13da3-362d-4998-abba-9d1d72bdb583" />

## Configure the S3 bucket for static website hosting with `index.html` as the index document.

<img width="1288" height="572" alt="image" src="https://github.com/user-attachments/assets/0edf65d6-cd8c-48d9-9014-4bc3628139d5" />

<img width="1803" height="705" alt="image" src="https://github.com/user-attachments/assets/35f89223-fccc-4a43-9b70-ec461646049f" />

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::xfusion-web-22236/*"
        }
    ]
}
```


## Allow public access to the bucket so that the website is publicly accessible.

<img width="1497" height="543" alt="image" src="https://github.com/user-attachments/assets/33242e8e-66e9-41f4-83cf-b8aa8cd426c6" />

<img width="1826" height="488" alt="image" src="https://github.com/user-attachments/assets/bfd4d403-e40d-4704-ad28-0f0eb2f03497" />


## Upload the `index.html` file from the `/root/` directory of the AWS client host to the S3 bucket.

```
aws s3 cp index.html s3://xfusion-web-22236/
```

<img width="1561" height="352" alt="image" src="https://github.com/user-attachments/assets/44b8c602-5cc8-4a98-bedf-fa42c6603387" />


## Verify that the website is accessible directly through the S3 website URL.

<img width="1808" height="481" alt="image" src="https://github.com/user-attachments/assets/20f654f2-670c-4326-a79c-efbe00e0f1f1" />

`Welcome to KKE labs!`


## Reference 

https://docs.aws.amazon.com/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html
