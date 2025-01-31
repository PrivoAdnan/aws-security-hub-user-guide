# Configuring an EventBridge rule for automatically sent findings<a name="securityhub-cwe-all-findings"></a>

You can create a rule in EventBridge that defines an action to take when a **Security Hub Findings \- Imported** event is received\. **Security Hub Findings \- Imported** events are triggered by updates from both [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) and [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html)\.

Each rule contains an event pattern, which identifies the events that trigger the rule\. The event pattern always contains the event source \(`aws.securityhub`\) and the event type \(**Security Hub Findings \- Imported**\)\. The event pattern can also specify filters to identify the findings that the rule applies to\.

The rule then identifies the rule targets\. The targets are the actions to take when EventBridge receives a **Security Hub Findings \- Imported** event and the finding matches the filters\.

The instructions provided here use the EventBridge console\. When you use the console, EventBridge automatically creates the required resource\-based policy that enables EventBridge to write to CloudWatch Logs\.

You can also use the [https://docs.aws.amazon.com/eventbridge/latest/APIReference/API_PutRule.html](https://docs.aws.amazon.com/eventbridge/latest/APIReference/API_PutRule.html) API operation of the EventBridge API\. However, if you use the EventBridge API, then you must create the resource\-based policy\. For details on the required policy, see [CloudWatch Logs permissions](https://docs.aws.amazon.com/eventbridge/latest/userguide/resource-based-policies-eventbridge.html#cloudwatchlogs-permissions) in the *Amazon EventBridge User Guide*\.

## Format of the event pattern<a name="securityhub-cwe-all-findings-rule-format"></a>

The format of the event pattern for **Security Hub Findings \- Imported **events is as follows:

```
{
  "source": [
    "aws.securityhub"
  ],
  "detail-type": [
    "Security Hub Findings - Imported"
  ],
  "detail": {
    "findings": {
      <attribute filter values>
    }
  }
}
```
+ `source` identifies Security Hub as the service that generates the event\.
+ `detail-type` identifies the type of event\.
+ `detail` is optional and provides the filter values for the event pattern\. If the event pattern does not contain a `detail` field, then all findings trigger the rule\.

You can filter the findings based on any finding attribute\. For each attribute, you provide a comma\-separated array of one or more values\.

```
"<attribute name>": [ "<value1>", "<value2>"]
```

If you provide more than one value for an attribute, then those values are joined by `OR`\. A finding matches the filter for an individual attribute if the finding has any of the listed values\. For example, if you provide both `INFORMATIONAL` and `LOW` as values for `Severity.Label`, then the finding matches if it has a severity label of either `INFORMATIONAL` or `LOW`\.

The attributes are joined by `AND`\. A finding matches if it matches the filter criteria for all of the provided attributes\.

When you provide an attribute value, it must reflect the location of that attribute within the AWS Security Finding Format \(ASFF\) structure\.

In the following example, the event pattern provides filter values for `ProductArn` and `Severity.Label`, so a finding matches if it is generated by Amazon Inspector and it has a severity label of either `INFORMATIONAL` or `LOW`\.

```
{
    "source": [
        "aws.securityhub"
     ],
    "detail-type": [
        "Security Hub Findings - Imported"
    ],
    "detail": {
        "findings": {
            "ProductArn": ["arn:aws:securityhub:us-east-1::product/aws/inspector"],
            "Severity": {
                "Label": ["INFORMATIONAL", "LOW"]
            }
        }
    }
}
```

## Creating an event rule<a name="securityhub-cwe-all-findings-predefined-pattern"></a>

You can use a predefined event pattern or a custom event pattern to create a rule in EventBridge\. If you select a predefined pattern, EventBridge automatically fills in `source` and `detail-type`\. EventBridge also provides fields to specify filter values for the following finding attributes:
+ `AwsAccountId`
+ `Compliance.Status`
+ `Criticality`
+ `ProductArn`
+ `RecordState`
+ `ResourceId`
+ `ResourceType`
+ `Severity.Label`
+ `Types`
+ `Workflow.Status`

**To create an EventBridge rule**

1. Open the Amazon EventBridge console at [https://console\.aws\.amazon\.com/events/](https://console.aws.amazon.com/events/)\.

1. Using the following values, create an EventBridge rule that monitors finding events:
   + For **Rule type**, choose **Rule with an event pattern**\.
   + Choose how to build the event pattern\.    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-cwe-all-findings.html)
   + For **Target types**, choose **AWS service**, and for **Select a target**, choose a target such as an Amazon SNS topic or AWS Lambda function\. The target is triggered when an event is received that matches the event pattern defined in the rule\.

   For details about creating rules, see [Creating Amazon EventBridge rules that react to events](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-create-rule.html) in the *Amazon EventBridge User Guide*\.

## <a name="securityhub-cwe-all-findings-custom-pattern"></a>