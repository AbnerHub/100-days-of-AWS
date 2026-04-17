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

1) Access to S3 Service on the AWS Console and choose create bucket.
2) Name your bucket the name `xfusion-web-22236 and leave the default settings
   
<img width="1340" height="678" alt="image" src="https://github.com/user-attachments/assets/bce13da3-362d-4998-abba-9d1d72bdb583" />


## Configure the S3 bucket for static website hosting with `index.html` as the index document.

After create your bucket you can enable static website hosting for your bucket.

1. Access to your bucket and go to **properties**
2. Under **Static Website hosting** chose edit
3. **Enable** static website hosting.
4. Under **index document** write the file name o the index document, typically *index.html*. 

<img width="1288" height="572" alt="image" src="https://github.com/user-attachments/assets/0edf65d6-cd8c-48d9-9014-4bc3628139d5" />



## Add a bucket policy 

After you edit S3 Block Public Access settings, you can add a bucket policy to grant public read access to your bucket

1. on S3 service, choose your bucket.
2. Choose **permissions**
3. Under **Bucket Policy**, choose edit

<img width="1803" height="705" alt="image" src="https://github.com/user-attachments/assets/35f89223-fccc-4a43-9b70-ec461646049f" />

4. To grant public read access for your website, copy the following bucket policy, and paste it in the **Bucket policy editor**.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::<Bucket-name>/*"
        }
    ]
}
```


## Allow public access to the bucket so that the website is publicly accessible.


By default, Amazon S3 blocks public access to your account and buckets. If you want to use a bucket to host a static website,
you can use these steps to edit your block public access settings.

1. Go to S3 service and select your bucket
2. Choose **permisions**
3. Under **block public access**
   
<img width="1826" height="488" alt="image" src="https://github.com/user-attachments/assets/bfd4d403-e40d-4704-ad28-0f0eb2f03497" />


4.Clear **Block all public access** and save the changes.


<img width="1497" height="543" alt="image" src="https://github.com/user-attachments/assets/33242e8e-66e9-41f4-83cf-b8aa8cd426c6" />


## Upload the `index.html` file from the `/root/` directory of the AWS client host to the S3 bucket.

There is a file name `index.html`  on your `aws-cli` client we need to upload this file to s3. 

1. Using the next command line we can upload the file to `xfusion-web-22236`

```
aws s3 cp index.html s3://xfusion-web-22236/
```

To Verify that the file was upload successfully

1. Access to your bucket
2. Go to **objects**. Here, you´ll see the file. 

<img width="1561" height="352" alt="image" src="https://github.com/user-attachments/assets/44b8c602-5cc8-4a98-bedf-fa42c6603387" />


## Verify that the website is accessible directly through the S3 website URL.

Once the static website bucket has been done, you can test your website endpoint.

1. Access to S3 service and select your bucket
2. go to **propieties**
3. UNder **Static Webstise hosting** copy the endpoint **URL**
4. Paste the endpoint in a browser window.

<img width="1808" height="481" alt="image" src="https://github.com/user-attachments/assets/20f654f2-670c-4326-a79c-efbe00e0f1f1" />


You will see the next message `Welcome to KKE labs!`


## 🔗 Reference 

https://docs.aws.amazon.com/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html
