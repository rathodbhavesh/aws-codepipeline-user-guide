# Create a CloudWatch Events rule for an Amazon S3 source \(console\)<a name="create-cloudtrail-S3-source-console"></a>

Before you set up a rule in CloudWatch Events, you must create an AWS CloudTrail trail\. For more information, see [Creating a Trail in the Console](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-create-a-trail-using-the-console-first-time.html)\.

**Important**  
If you use the console to create or edit your pipeline, your CloudWatch Events rule and AWS CloudTrail trail are created for you\.

**To create a trail**

1. Open the AWS CloudTrail console\.

1. In the navigation pane, choose **Trails**\.

1. Choose **Create trail**\. For **Trail name**, enter a name for your trail\.

1. Under **Storage location**, create or specify the bucket to be used to store the log files\. By default, Amazon S3 buckets and objects are private\. Only the resource owner \(the AWS account that created the bucket\) can access the bucket and its objects\. The bucket must have a resource policy that allows AWS CloudTrail permissions to access the objects in the bucket\.

1. Under **Trail log bucket and folder**, specify an Amazon S3 bucket and the object prefix \(folder name\) to log data events for all objects in the folder\. For each trail, you can add up to 250 Amazon S3 objects\. Complete the required encryption key information and choose **Next**\.

1. For **Event type**, choose **Management events**\.

1. For **Management events**, choose **Write**\. The trail records Amazon S3 object\-level API activity \(for example, `GetObject` and `PutObject`\) on the specified bucket and prefix\.

1. Choose **Write**\. 

1. If you're satisfied with the trail, choose **Create trail**\.

**To create a CloudWatch Events rule that targets your pipeline with an S3 source**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Events**, and then choose **Rules**\. Choose **Create rule**\.

1. Choose **Event Pattern**, and then choose **Build event pattern to match events by service**\.

1. Under **Event source**, from **Service Name**, choose **Simple Storage Service \(S3\)**\.

1. From **Event Type**, choose **Object Level Operations**\.

1. 

   Choose **Specific operation\(s\)**, and then choose **CompleteMultipartUpload**, **CopyObject**, and **PutObject**\.

   Above the **Event Pattern Preview** pane, choose **Edit**\. Edit the event pattern to add the bucket name and S3 object key \(or key name\) which uniquely identifies the object in the bucket as `requestParameters`\. In this example, a rule is created for a bucket named `my-bucket` and an object key of `my-files.zip`\. When you use the **Edit** window to specify resources, your rule is updated to use a custom event pattern\.

   The following is a sample event pattern to copy and paste:

   ```
   {
       "source": [
           "aws.s3"
       ],
       "detail-type": [
           "AWS API Call via CloudTrail"
       ],
       "detail": {
           "eventSource": [
               "s3.amazonaws.com"
           ],
           "eventName": [
               "CopyObject",
               "CompleteMultipartUpload",
               "PutObject"
           ],
           "requestParameters": {
               "bucketName": [
                   "my-bucket"
               ],
               "key": [
                   "my-files.zip"
               ]
           }
       }
   }
   ```

1. In **Targets**, choose **CodePipeline**\.

1. Enter the pipeline ARN for the pipeline to be started by this rule\.
**Note**  
To get the pipeline ARN, run the get\-pipeline command\. The pipeline ARN appears in the output\. It is constructed in this format:   
arn:aws:codepipeline:*region*:*account*:*pipeline\-name*  
Sample pipeline ARN:  
arn:aws:codepipeline:us\-east\-2:80398EXAMPLE:MyFirstPipeline 

1. To create or specify an IAM service role that grants Amazon CloudWatch Events permissions to invoke the target associated with your Amazon CloudWatch Events rule \(in this case, the target is CodePipeline\): 
   + Choose **Create a new role for this specific resource** to create a service role that gives Amazon CloudWatch Events permissions to your start your pipeline executions\.
   + Choose **Use existing role** to enter a service role that gives Amazon CloudWatch Events permissions to your start your pipeline executions\.

1. Review your rule to make sure it meets your requirements, and then choose **Configure details**\.

1. On the **Configure rule details** page, enter a name and description for the rule, and then choose **State** to enable the rule\.

1. If you're satisfied with the rule, choose **Create rule**\.