+++
title = "Walkthrough"
chapter = true
weight = 40
+++

The solution automates the setup and deployment in two steps:

**Step 1**: In the AWS CloudFormation console, [create a stack](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-console-create-stack.html#cfn-using-console-initiating-stack-creation) to launch the [aws-auditmanager-securityhub.yml](https://github.com/aws-samples/aws-securityhub-remediations/blob/main/aws-auditmanager-securityhub/cft/aws-auditmanager-securityhub.yml) template. In *Parameters*, enter the values for the parameters based on their descriptions in the template. The template takes the following parameters: 

*SourceBucket*: The name of the S3 bucket that contains the AWS Lambda source code. This is the bucket you created in step 4 of the prerequisites. Replace <AccountID> and <Region> with the AWS account ID and Region where you are deploying this template.

**Step 2**: In the AWS CloudFormation console, create a stack to launch the [aws-auditmanager-customassessment.yml](https://github.com/aws-samples/aws-securityhub-remediations/blob/main/aws-auditmanager-securityhub/cft/aws-auditmanager-customassessment.yml) template. In *Parameters*, enter the values for the parameters based on their descriptions in the template. The template takes the following parameters: 

*AssessmentDestination*: The S3 URI in which AWS Audit Manager will save your assessment reports. This is the S3 URI from step 7 of the prerequisites. Replace <AccountID> and <Region> with the AWS account ID and Region where you are deploying this template.
*AuditOwnerArn*: The ARN for the IAM user you created in step 6 of the prerequisites.


**Review Setup**

1. Navigate to *AWS Audit Manager console*. On the left hand panel, choose *Control library*. On the right hand panel, choose *Custom Control*. You will see a list of custom controls that have been created for you.
![AWS Logo](/images/cft/12.PNG)

2. On the left hand panel, choose *Framework Library*. On the right hand panel, choose *Custom Framework*. You will see a custom Framework has been created for you.
![AWS Logo](/images/cft/17.PNG)

3. Select the custom framework named *Security Hub Custom Framework*.  Under the *Control* section, you will see that this framework incorporates custom controls you previously encountered in the *Custom Control* tab
![AWS Logo](/images/cft/18.PNG)

4. On the left hand panel, choose *Assessments*. You will see a custom Assessment has been created for you.
![AWS Logo](/images/cft/10.PNG)

5. Select the assement named *CustomSecurityHubAssessment*.
![AWS Logo](/images/cft/19.PNG)

In the above figure, on the *Control* section, see that Assessment has started to record evidence under "Total evidence". It might take 24 hours for the evidence to appear.

For AWS Security Hub, the frequency of evidence collection follows the schedule of your AWS Security Hub checks. To start evidence collection, AWS Audit Manager assesses an in-scope resource from a data source (in this case, a related Security Hub compliance check result). It converts the obtained data into an auditor-friendly format to make it easier to understand. The converted data and metadata are then saved as Audit Manager evidence and attached to each control of the control set in the assessment. Now that your deployment is complete, you can review the evidence collected from your custom assessment.