<p align="center">
</p>

# Automated, Real Time Remediations for Foundational Security Benchmarks using AWS Security Hub

AWS provides built-in automated detection of Foundational Security violations via 2 distinct mechanisms - AWS Config Rules or via AWS Security Hub ( that internally leverages Config). However, there's no built-in support for remediations. 

These templates provide real time and automated remediations for each of the Foundational Security benchmarks by providing a fully automated integration of AWS Security Hub Custom Actions and AWS Systems Manager automation documents.


## How it Works

1. Leverages AWS Security Hub directly to provide automated detection of Foundational Security findings
2. Provides NEW AWS Systems Manager Automation Documents for automated remediation for AWS Security Hub Foundational Security findings. All documents are automatically provisioned via a AWS CloudFormation template.
3. Provides NEW integration of AWS Security Hub Custom Actions with AWS Systems Manager Automation Documents to provide real time remediations of AWS Security Hub Foundational Security findings. Provisions Event based (CloudWatch Events) processing of AWS Security Hub Findings based on the AWS Security Hub Finding Format (ASFF) and packages the finding as input parameters for the associated AWS Systems Manager Automation Document.

## Solution Design

![Solution Design](https://github.com/kmmahaj/config/blob/master/aws-auto-remediate-fsbp-securityhub/images/arch-diagram.png)

## How To Install

1. **Template 1 of 2:** aws-fsbp-systemsmanagerautomations.yml
* Provisions AWS Systems Manager automation documents. These documents are used to provide automated remediations within the provisioned AWS Security Hub Action.
* Provisions with fully built-in pre-reqs. No input parameters required. Simply install on the CloudFormation console (or CLI). Installs in approx 3-4 mins.

2. **Template 2 of 2:** aws-fsbp-securityhubactions.yml
* Provisions AWS CloudWatch Evemts and AWS Security Hub Custom Actions. No input parameters. Simply install on the CloudFormation console (or CLI). Installs in approx 3-4 mins.
* Leverages the output from the previous template specifically the AWS Systems Manager Automation documents

## COVERAGE

The [Coverage Matrix](https://github.com/kmmahaj/config/blob/master/aws-auto-remediate-fsbp-securityhub/coverage/AWS%20SecurityHub%20Benchmarks-Coverage-v1.xlsx) provides the current coverage of this solution wrt the FSBP Benchmarks

## Author

Kanishk Mahajan; kmmahaj@amazon.com

