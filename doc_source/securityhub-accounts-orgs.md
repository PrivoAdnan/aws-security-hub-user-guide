# Managing member accounts that belong to an organization<a name="securityhub-accounts-orgs"></a>

For organization accounts, the Security Hub administrator account can perform the following actions:
+ Enable organization accounts as Security Hub member accounts\.
+ Automatically enable new organization accounts as they are added to the organization\.
+ Disassociate accounts that belong to the organization\. They cannot delete organization accounts\. 

To ensure that the administrator account has the required permissions to manage the organization accounts, attach the following managed policies to the associated IAM principal\.
+ [`AWSSecurityHubFullAccess`](security-iam-awsmanpol.md#security-iam-awsmanpol-awssecurityhubfullaccess)
+ [`AWSSecurityHubOrganizationsAccess`](security-iam-awsmanpol.md#security-iam-awsmanpol-awssecurityhuborganizationsaccess)

If the administrator account has not enabled the option to automatically enable new organization accounts, then the **Accounts** page displays a message at the top of the page\. The message contains an **Enable** option\.

When you choose **Enable**, Security Hub performs the following actions:
+ Enables all of the current organization accounts as member accounts\.
+ For those accounts, enables the CIS AWS Foundations Benchmark standard and the AWS Foundational Best Practices standard\.
+ Enables the option to automatically enable new accounts as they are added to the organization\.

**Topics**
+ [Automatically enabling new organization accounts](accounts-orgs-auto-enable.md)
+ [Enabling member accounts from your organization](orgs-accounts-enable.md)
+ [Disassociating member accounts from your organization](accounts-orgs-disassociate.md)