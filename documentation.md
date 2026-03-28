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
### Setting up AWS and Terraform
I started this project by launching my Linux Debian virtualmachine. I created local directory to store AWS credentials by using command `mkdir ~/.aws`, this is the standard path where the AWS CLI and Terraform will look for the credentials.  

Next, I created file for the credentials by using command `nano ~/.aws/credentials` and added my access key, secret access key and session token locally.  

![pic1](./Pictures/pic1.png)  

Next, I installed AWS CLI in my local Linux machine by using command `sudo apt install awscli`. First time I tried command `aws --version` I got error that my credentials file was not working correctly. I made small change in credentials file (added [default] as first line in file) and got it working.  

![pic2](./Pictures/pic2.png)  

![pic3](./Pictures/pic3.png)  
Credentials working correctly.  

Next, I installed Terraform. Install guide can be found here: https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli  

![pic4](./Pictures/pic4.png)  

### Starting Terraform project
I started Terraform project by creating new repository in Github and cloning it to the local mahcine. After this I opened file named provider.tf in VSCode. After providing region and profile to the file I saved it and used command `terraform init` to see if Terraform works with AWS.  

![pic5](./Pictures/pic5.png)  

Next, I added this line in the provider.tf -file: `data "aws_caller_identity" "current" {}`. This tells Terraform who the AWS user is.  

Now I am ready to test creating S3 bucket with Terraform. I created file named main.tf and opened it in VSCode.  

![pic6](./Pictures/pic6.png)  

`terraform plan` gives no errors so I created also the output bucket using same logic. Next, I tried the `terraform apply` and checked if the S3 buckets are created.  

![pic7](./Pictures/pic7.png)  

![pic8](./Pictures/pic8.png)  
S3 buckets are created.  



## Enhancements

### References
