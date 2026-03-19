![Status](https://img.shields.io/badge/Status-In%20Progress-yellow?style=for-the-badge&logo=gitbook&logoColor=white)

![Technical Challenge](https://img.shields.io/badge/Challenge-Troubleshooting%20Solved-007ACC?style=for-the-badge&logo=visual-studio-code&logoColor=white)
# # AWS S3 Static Website Hosting (CLI Project)

![AWS](https://img.shields.io/badge/AWS-Cloud-orange)
![S3](https://img.shields.io/badge/Amazon-S3-green)
![IAM](https://img.shields.io/badge/Identity-IAM-red)
![CLI](https://img.shields.io/badge/Interface-CLI-lightgrey)
![Script](https://img.shields.io/badge/Automation-Bash-blueviolet)

## Project Description

This project demonstrates how to deploy a static website using Amazon S3 and AWS CLI.

The project is based on a guided lab, but it was fully adapted and implemented in a personal AWS account. Several modifications were required to replicate the lab environment, including manual configuration of IAM users, CLI setup, and S3 permissions.

---

## The goal of this project is to understand how to:

- Deploy a static website using Amazon S3
- Use AWS CLI for resource management
- Configure IAM users and access keys
- Understand and apply bucket policies
- Troubleshoot real-world AWS permission issues

## Architecture

User (Browser) 

↓  
HTTP Request  
↓  
Amazon S3 Bucket (Static Website Hosting)
          

## AWS Services Used

| Service | Purpose |
|--------|--------|
| Amazon S3 | Static website hosting |
| AWS CLI | Resource management |
| IAM | User and access management |
| HTML/CSS Template | Website content |

## Prerequisites

Before starting this project, the following requirements are needed:

- An active AWS account
- Basic knowledge of Linux commands
- IAM user with programmatic access (Access Key & Secret Key)
- A terminal environment (e.g., VS Code, Codespaces, or local machine)
- Internet connection

Optional:
- Basic understanding of cloud computing concepts

## 🚀 Steps Overview

1. Create an IAM user with programmatic access
2. Install and configure AWS CLI
3. Create an S3 bucket
4. Disable Block Public Access settings
5. Apply a bucket policy for public read access
6. Upload static website files to S3
7. Enable static website hosting
8. Verify deployment and access the website

## Implementation Steps
## 1 Create an S3 Bucket

Create a bucket using the AWS CLI.

aws s3api create-bucket
--bucket my-static-site-bucket
--region us-west-2
--create-bucket-configuration LocationConstraint=us-west-2

## 2 Create an IAM User

Create a new IAM user that will manage the S3 bucket.

aws iam create-user --user-name awsS3user

Attach the S3 full access policy.

aws iam attach-user-policy
--policy-arn arn:aws:iam::aws/AmazonS3FullAccess
--user-name awsS3user

## 3 Enable Static Website Hosting

Configure the bucket to host a static website.

aws s3 website s3://my-static-site-bucket/
--index-document index.html

## 4 Upload Website Files

Upload the static website files.

aws s3 cp website/ s3://my-static-site-bucket/
--recursive
--acl public-read

## 5 Verify Files

aws s3 ls s3://my-static-site-bucket/

## 6 Access the Website

http://my-static-site-bucket.s3-website-us-west-2.amazonaws.com

## Automation Script

To automate updates, create the following script.

scripts/update-website.sh

#!/bin/bash

aws s3 cp website/ s3://my-static-site-bucket/
--recursive
--acl public-read

Make it executable.

chmod +x update-website.sh

Run the script to deploy changes.

./update-website.sh

## What I Learned

* How to create a virtual machine in AWS
* How SSH authentication works
* Basic Linux server management
* Cloud infrastructure fundamentals

## Future Improvements

- Integrate Amazon CloudFront for content delivery (CDN)
- Add a custom domain with Route 53
- Enable HTTPS using SSL/TLS certificates
- Automate deployment using scripts or Infrastructure as Code (IaC)
- Improve security by restricting public access using advanced configurations

## Author

Miguel Bocanegra

