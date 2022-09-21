# Disabling Security Hub<a name="securityhub-disable"></a>

To disable AWS Security Hub, you can use the Security Hub console or the Security Hub API\.

You cannot disable Security Hub in the following cases:
+ Your account is the designated Security Hub administrator account for an organization\.
+ Your account is a Security Hub administrator account by invitation, and you have member accounts that are enabled\. Before you can disable Security Hub, you must disassociate all of your member accounts\. See [Disassociating member accounts](securityhub-disassociate-members.md)\.
+ Your account is a member account\. Before you can disable Security Hub, your account must be disassociated from your administrator account\.

  For an organization account, only the administrator account can disassociate member accounts\. See [Disassociating member accounts from your organization](accounts-orgs-disassociate.md)\.

  For manually invited accounts, either the administrator account or the member account can disassociate the member account\. See [Disassociating member accounts](securityhub-disassociate-members.md) or [Disassociating from your administrator account](securityhub-disassociate-from-admin.md)\.

When you disable Security Hub for an account, it is disabled only in the current Region\. No new findings are processed for the account in that Region\.

The following also occurs\.
+ After 90 days, your existing findings and insights and any Security Hub configuration settings are deleted and cannot be recovered\.

  If you want to save your existing findings, you must export them before you disable Security Hub\. For more information, see [Effect of account actions on Security Hub data](securityhub-data-retention.md)\.
+ Any enabled standards are disabled\.

## Disabling Security Hub \(console\)<a name="securityhub-disable-console"></a>

You can disable Security Hub from the AWS Management Console\.

**To disable Security Hub \(console\)**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Settings**\.

1. On the **Settings** page, choose **General**\.

1. Under **Disable AWS Security Hub**, choose **Disable AWS Security Hub**\. Then choose **Disable AWS Security Hub** again\.

## Disabling Security Hub \(Security Hub API, AWS CLI\)<a name="securityhub-disable-api"></a>

To disable Security Hub, you can use an API call or the AWS Command Line Interface\.

**To disable Security Hub \(Security Hub API, AWS CLI\)**
+ **Security Hub API** – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DisableSecurityHub.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_DisableSecurityHub.html) operation\.
+ **AWS CLI** – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/disable-security-hub.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/disable-security-hub.html) command\.

  ```
  aws securityhub disable-security-hub
  ```