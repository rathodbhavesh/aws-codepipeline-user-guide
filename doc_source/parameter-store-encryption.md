# Use AWS Secrets Manager to track database passwords or third\-party API keys<a name="parameter-store-encryption"></a>

We recommend that you use AWS Secrets Manager to rotate, manage, and retrieve database credentials, API keys, and other **secrets** throughout their lifecycle\. Secrets Manager enables you to replace hardcoded credentials in your code \(including passwords\) with an API call to Secrets Manager to retrieve the secret programmatically\. For more information, see [What Is AWS Secrets Manager?](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html) in the *AWS Secrets Manager User Guide*\.

For pipelines where you pass parameters that are secrets \(such as OAuth credentials\) in an AWS CloudFormation template, you should include dynamic references in your template that access the secrets you have stored in Secrets Manager\. For the reference ID pattern and examples, see [Secrets Manager Secrets](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/dynamic-references.html#dynamic-references-secretsmanager) in the *AWS CloudFormation User Guide*\. For an example that uses dynamic references in a template snippet for GitHub webhook in a pipeline, see [Webhook Resource Configuration](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-codepipeline-webhook.html#aws-resource-codepipeline-webhook--examples)\.



## See also<a name="related-resources-managing-secrets"></a>

The following related resources can help you as you work with managing secrets\.
+ Secrets Manager can rotate database credentials automatically, such as for rotation of Amazon RDS secrets\. For more information, see [Rotating Your AWS Secrets Manager Secrets](https://docs.aws.amazon.com/secretsmanager/latest/userguide/rotating-secrets.html) in the *AWS Secrets Manager User Guide*\.
+ To view instructions for adding Secrets Manager dynamic references to your AWS CloudFormation templates, see [https://aws.amazon.com/blogs/security/how-to-create-and-retrieve-secrets-managed-in-aws-secrets-manager-using-aws-cloudformation-template/](https://aws.amazon.com/blogs/security/how-to-create-and-retrieve-secrets-managed-in-aws-secrets-manager-using-aws-cloudformation-template/)\. 