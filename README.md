# AWS S3 Static Website Deployment using AWS CLI
## Project Description

This project demonstrates how to deploy a static website using Amazon S3 and manage resources using the AWS CLI.

The goal of this project is to understand how to:

Create and configure an S3 bucket

Manage permissions using IAM

Upload files using AWS CLI

Host a static website on Amazon S3

Automate website updates using a Bash script

## Architecture

User
|
Internet
|
Amazon S3 Bucket
|
Static Website

## AWS Services Used

Amazon S3

AWS IAM

AWS CLI

Amazon EC2

## Prerequisites

Before starting this project you need:

AWS account

AWS CLI configured

Basic Linux knowledge

SSH access to an EC2 instance

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

Using AWS CLI to manage AWS resources

Deploying static websites using Amazon S3

Managing IAM users and permissions

Automating deployments using Bash scripts

## Future Improvements

Use AWS CloudFront as a CDN

Add a custom domain

Implement CI/CD with GitHub Actions

## Author

Miguel Bocanegra

