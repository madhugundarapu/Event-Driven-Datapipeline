#Event-Driven-Datapipeline
## Project Overview

This project builds an **event-driven data pipeline on AWS** using:

- AWS Lambda to process and generate daily summary reports
- Amazon S3 to store reports
- AWS CloudWatch Events to trigger Lambda daily
- AWS SES to email reports (optional)
- Terraform for Infrastructure as Code (IaC)
- Jenkins for Continuous Integration and Deployment (CI/CD)



## Project Structure


event-driven-pipeline/
├── terraform/
│   ├── main.tf
│   ├── variables.tf
│   ├── provider.tf
├── lambda/
│   └── process_event.py
├── Jenkinsfile

project-root/ 
├── terraform/
│   ├── main.tf
│   ├── variables.tf
│   ├── provider.tf
├── lambda/
│   └── process_event.py
├── Jenkinsfile
├── README.md


## Deployment Instructions

### Prerequisites

- AWS CLI configured with IAM credentials
- Terraform installed
- Jenkins installed with AWS credentials
- Verified email in AWS SES
- IAM user with `AdministratorAccess` (or relevant policies)

### 1.Prepare the Lambda Function

bash
cd lambda
zip process_event.zip process_event.py


### 2. Initialize & Deploy Terraform

bash
cd terraform
terraform init
terraform apply -auto-approve


### 3. Jenkins CI/CD Setup

- Create a new Jenkins Pipeline job
- Use the provided `Jenkinsfile`
- Configure AWS credentials in Jenkins (use `aws-access-key` and `aws-secret-key` ID names)

### 4. Trigger the Build

- Push changes to the Git repo or manually build the pipeline
- Jenkins will deploy the Lambda and infra automatically

## Monitoring & Dashboard

Create a CloudWatch Dashboard:

1. Go to CloudWatch > Dashboards
2. Add widgets for:
   - Lambda invocations & errors
   - S3 putObject activity
   - SES email delivery stats


## SES Email Setup (Optional)

1. Verify an email address in AWS SES
2. Replace `verified_email@example.com` and `recipient@example.com` in `process_event.py`
3. Enable Production access in SES to send to external recipients


## 🧹 Cleanup

bash
terraform destroy -auto-approve
