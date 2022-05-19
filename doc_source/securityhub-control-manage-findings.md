# Viewing and taking action on control findings<a name="securityhub-control-manage-findings"></a>

The control details page contains a list of active findings for the control\. The list does not include archived findings\.

The control details page does not support cross\-Region aggregation\. The control details page only displays findings from the current Region\.

The list provides tools to filter and sort the findings, so that you can focus on more urgent findings first\. Each finding can include links to resource details in the related service console\. For controls that are based on AWS Config rules, you can view details about the rule and the configuration timeline\.

You can also use the AWS Security Hub API to retrieve a list of findings\. See [Retrieving finding details \(Security Hub API, AWS CLI\)](finding-retrieve-api-cli.md)\.

**Topics**
+ [Filtering, sorting, and downloading the control finding list](control-finding-list.md)
+ [Viewing details about a control finding and finding resource](control-finding-resource-details.md)
+ [Taking action on control findings](control-finding-take-action.md)