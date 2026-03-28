Date 28.3.2026  
Thomas Punnala  
# Data processing pipeline in AWS

## Introduction
This project implements a simple serverless file processing architecture in Amazon Web Services using Infrastructure as Code with Terraform. The goal is to deploy small cloud-based solution that can automatically process files uploaded to cloud storage.  
In this architecture files uploaded to an Amazon S3 bucket trigger and AWS lambda function. The lambda function processes the file (counts words and lines inside of the text file and adds timestamp) and stores the result in seperate S3 output bucket. Additionally an Amazon SNS topic is used to send notification when processing is completed.  
The main objective is to gain experience in simple event driven cloud architecture, deploying infrastructure using Terraform and using AWS managed services S3, Lambda, and SNS.  

## Resources
S3  
Lambda  
SNS  

## Design
This architecture is based on an event driven serverless model. When file is uploaded to an S3 input bucket, and event triggers a Lambda function that processes the file and stores the result in an S3 output bucket. After processing the function sends a notification via SNS.  
Serverless approach was chosen to reduce operational complexity. AWS lambda eliminates the need to manage servers and allows automatic scaling based on events.  
There is also no VPC usage. All selected services are fully managed AWS services that operate outside of user defined VPC by default. Adding a VPC would add unnecessary complexity without providing additional benefits in this project.  
Terraform is used to define and deploy the infrastructure as code. This allows the enviroment to be recreated quickly.  
Seperate S3 buckets are used to keep architecture clear and also makes it easier to manage permissions and lifecycle policies in future.  
Because the system is event driven it triggers only when new data is uploaded. This reduces cost and improves efficiency.  

## Implementation

## Enhancements

### References
