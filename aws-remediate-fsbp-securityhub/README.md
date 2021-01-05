<p align="center">
</p>

# Automated Remediations for Foundational Security Benchmarks using AWS Security Hub

The AWS Foundational Security Best Practices (FSBP) standard is a set of controls that detect when your deployed accounts and resources deviate from AWS security best practices.

The solution implemented here leverages the AWS Security Hub service and provides customers with an AWS native implementation for automated remediations for these FSBP violations detected by AWS Security Hub.


## How it Works

This implementation is based on the following solution approach:

1. Leverages AWS Security Hub directly to provide continuous detection of FSBP findings
2. Provides AWS Systems Manager Automation Documents for automated remediation for AWS Security Hub findings. All documents are automatically provisioned via an AWS CloudFormation template.
3. Provides integration of AWS Security Hub Custom Actions with AWS Systems Manager Automation Documents to provide real time remediations of AWS Security Hub FSBP findings as follows:
* Leverages the ability of AWS Security Hub to send findings associated with custom actions to CloudWatch Events as Security Hub Findings - Custom Action events.
* The CloudWatch Events Rule invokes the corresponding Lambda Function as the Target for the source Security Hub Custom Action event
* The Lambda function processes the finding using the standard findings format provided by Security Hub - AWS Security Finding Format (ASFF) and invokes the corresponding AWS Systems Manager Automation Document with the input from the ASFF finding


## Solution Design

![](images/arch-diagram.png)

## How To Install

1. **Template 1 of 2:** aws-security-hub-fsbp-remediations-template1.yml
* Provisions AWS Systems Manager automation documents. These documents are used to provide automated remediations within the provisioned AWS Security Hub Action.
* Provisions with fully built-in pre-reqs. No input parameters required. Simply install on the CloudFormation console (or CLI). Installs in approx 3-4 mins.

2. **Template 2 of 2:** aws-security-hub-fsbp-remediations-template2.yml
* Provisions AWS CloudWatch Evemts and AWS Security Hub Custom Actions. No input parameters. Simply install on the CloudFormation console (or CLI). Installs in approx 3-4 mins.
* Leverages the output from the previous template specifically the AWS Systems Manager Automation documents

## COVERAGE

The solution provides remediations for the following AWS Security Hub FSBP checks:
* [EC2.3] Attached EBS volumes should be encrypted at-rest
* [GuardDuty.1] GuardDuty should be enabled
* [IAM.3] IAM users' access keys should be rotated every 90 days or less
* [Lambda.1] Lambda functions should prohibit public access by other accounts
* [Lambda.2] Lambda functions should use latest runtimes
* [RDS.3] RDS DB instances should have encryption at-rest enabled
* [SSM.1] EC2 instances should be managed by AWS Systems Manager

Additionally coverage for remediations for the following Foundational Security Best Practices Controls is also provided by this solution due to the coverage for remediations for PCI Controls:
* [AutoScaling.1] Auto Scaling groups associated with a load balancer should use load balancer health checks
* [CloudTrail.1] CloudTrail should be enabled and configured with at least one multi-Region trail
* [CloudTrail.2] CloudTrail should have encryption at-rest enabled
* [CodeBuild.2] CodeBuild project environment variables should not contain clear text credentials
* [Config.1] AWS Config should be enabled
* [EC2.1] Amazon EBS snapshots should not be public, determined by the ability to be restorable by anyone
* [EC2.2] The VPC default security group should not allow inbound and outbound traffic
* [IAM.1] IAM policies should not allow full * administrative privileges
* [IAM.2] IAM users should not have IAM policies attached
* [IAM.4] IAM root user access key should not exist
* [IAM.7] Password policies for IAM users should have strong configurations
* [S3.1] S3 Block Public Access setting should be enabled
* [S3.2] S3 buckets should prohibit public read access
* [S3.3] S3 buckets should prohibit public write access
* [S3.4] S3 buckets should have server-side encryption enabled
* [RDS.1] RDS snapshots should be private
* [RDS.2] RDS DB instances should prohibit public access, determined by the PubliclyAccessible configuration
* [SSM.2] Amazon EC2 instances managed by Systems Manager should have a patch compliance status of COMPLIANT after a patch installation 

## @kmmahaj



