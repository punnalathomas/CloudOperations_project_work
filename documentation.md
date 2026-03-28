Date 28.3.2026  
Thomas Punnala  
# Data processing pipeline in AWS

## Introduction
This project implements a simple serverless file processing architecture in Amazon Web Services using Infrastructure as Code with Terraform. The goal is to deploy small cloud-based solution that can automatically process files uploaded to cloud storage.  
In this architecture files uploaded to an Amazon S3 bucket trigger and AWS lambda function. The lambda function processes the file (counts words and lines inside of the text file and adds timestamp) and stores the result in seperate S3 output bucket. Additionally an Amazon SNS topic is used to send notification when processing is completed.  
The main objective is to gain experience in simple event driven cloud architecture, deploying infrastructure using Terraform and using AWS managed services S3, Lambda, and SNS.  

## Resources

## Design

## Implementation

## Enhancements

### References
