# Day 35: Create a Lambd function using CLI 

## 📌 Overview
The Nautilus DevOps team continues to explore serverless architecture by setting up another Lambda function. 
This time, the task must be completed using the AWS Console to familiarize the team with the web interface. 
The function will return a custom greeting and demonstrate the capabilities of AWS Lambda effectively.
Create Python Script: Create a Python script named **lambda_function.py** with a function that returns the body *Welcome to KKE AWS Labs!* and status code **200.**
Zip the Python Script: Zip the script into a file named **function.zip.**
Create Lambda Function: Create a Lambda function named **nautilus-lambda-cli** using the zipped file and specify Python as the runtime.
IAM Role: Use the IAM role named **lambda_execution_role.**
Use AWS CLI which is already configured on the aws-client host.

## 🚀 Solution

1. Create a python script in a text editor, using vim or nano and write into it the 

```
import json

def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': json.dumps('Welcome to KKE AWS LABS !')
    }
```
2. Package the function created in step 1 as  .zip file

   ```
   zip function.zip lambda_function.py
   ```

3. There is a role that we´ll use **lambda_execution_role**, we need to know what is its ARN string to be used in the next step
   to discover it, we use the next command
   ```
   aws iam get-role --role-name lambda_execution_role --query 'Role.Arn' --output text
   #Output
   #arn:aws:iam::230270923096:role/lambda_execution_role
   ```


4. Create the lambda function, using .zip. IAM role and python script created in the previous steps

```
aws lambda create-function --function-name nautilus-lambda-cli \
--zip-file fileb://function.zip --handler lambda_function.lambda_handler --runtime python3.10.17 \
--role arn:aws:iam::230270923096:role/lambda_execution_role 
```
