# Viewing and taking action on insight results and findings<a name="securityhub-insights-view-take-action"></a>

For each insight, AWS Security Hub first determines the findings that match the filter criteria, and then uses the grouping attribute to group the matching findings\.

From the **Insights** console page, you can view and take action on the results and findings\.

If you enabled finding aggregation, then in the aggregation Region, the results for managed insights include findings from the aggregation Region and the linked Regions\. For custom insight results, if the insight does not filter by Region, then the results include findings from the aggregation Region and linked Regions\.

In other Regions, the insight results are only for that Region\.

For information on how to configure finding aggregation, see [Aggregating findings across Regions](finding-aggregation.md)\.

## Viewing and taking action on insight results \(console\)<a name="securityhub-insight-results-console"></a>

The insight results consist of a grouped list of the results for the insight\. For example, if the insight is grouped by resource identifiers, then the insight results are the list of resource identifiers\. Each item in the results list indicates the number of matching findings for that item\.

Note that if the findings are grouped by resource identifier or resource type, then the results include all of the resources in the matching findings\. This includes resources that have a different type from the resource type specified in the filter criteria\. For example, an insight identifies findings that are associated with S3 buckets\. If a matching finding contains both an S3 bucket resource and an IAM access key resource, then the insight results list both of those resources\.

The results list is sorted from most to fewest matching findings\.

Security Hub can only display 100 results\. If there are more than 100 grouping values, you only see the first 100\.

In addition to the results list, the insight results display a set of charts summarizing the number of matching findings for the following attributes\.
+ **Severity label** – Number of findings for each severity label
+ **AWS account ID** – Top five account IDs for the matching findings
+ **Resource type** – Top five resource types for the matching findings
+ **Resource ID** – Top five resource IDs for the matching findings
+ **Product name** \- Top five finding providers for the matching findings

If you have configured custom actions, then you can send selected results to a custom action\. The action must be associated with a CloudWatch rule for the `Security Hub Insight Results` event type\. See [Automated response and remediation](securityhub-cloudwatch-events.md)\.

If you have not configured custom actions, then the **Actions** menu is disabled\.

**To display and take action on the list of insight results**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Insights**\.

1. To display the list of insight results, choose the insight name\.

1. Select the check box for each result to send to the custom action\.

1. From the **Actions** menu, choose the custom action\.

## Viewing insight results \(Security Hub API, AWS CLI\)<a name="securityhub-insight-results-api"></a>

To view insight results, you can use an API call or the AWS Command Line Interface\.

**To view insight results \(Security Hub API, AWS CLI\)**
+ **Security Hub API** – Use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetInsightResults.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetInsightResults.html) operation\. To identify the insight to return results for, you need the insight ARN\. To obtain the insight ARNs for custom insights, use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetInsights.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetInsights.html) operation\.
+ **AWS CLI** – At the command line, run the [https://docs.aws.amazon.com/cli/latest/reference/securityhub/get-insight-results.html](https://docs.aws.amazon.com/cli/latest/reference/securityhub/get-insight-results.html) command\.

  ```
  aws securityhub get-insight-results --insight-arn <insight ARN>
  ```

  Example:

  ```
  aws securityhub get-insight-results --insight-arn "arn:aws:securityhub:us-west-1:123456789012:insight/123456789012/custom/a1b2c3d4-5678-90ab-cdef-EXAMPLE11111"
  ```

## Viewing findings for an insight result \(console\)<a name="securityhub-insight-findings-console"></a>

From the insight results list, you can display the list of findings for each result\.

**To display and take action on insight findings**

1. Open the AWS Security Hub console at [https://console\.aws\.amazon\.com/securityhub/](https://console.aws.amazon.com/securityhub/)\.

1. In the navigation pane, choose **Insights**\.

1. To display the list of insight results, choose the insight name\.

1. To display the list of findings for an insight result, choose the item from the results list\.

The findings list shows the active findings for the selected insight result that have a workflow status of `NEW` or `NOTIFIED`\.

From the findings list, you can perform the following actions\.
+ [Change the filters and grouping for the list](findings-filtering-grouping.md)
+ [View details for individual findings](finding-view-details.md)
+ [Update the workflow status of findings](finding-workflow-status.md)
+ [Send findings to custom actions](finding-send-to-custom-action.md)