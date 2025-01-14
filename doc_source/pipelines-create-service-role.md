# Create the CodePipeline service role<a name="pipelines-create-service-role"></a>

When you create a pipeline, you create a service role or use an existing service role\.

You can use the CodePipeline console or the AWS CLI to create a CodePipeline service role\. A service role is required to create a pipeline, and the pipeline is always associated to that service role\. 

Before you create a pipeline with the AWS CLI, you must create a CodePipeline service role for your pipeline\. For an example AWS CloudFormation template with the service role and policy specified, see the tutorials in [Tutorial: Create a pipeline that uses variables from AWS CloudFormation deployment actions](tutorials-cloudformation-action.md)\.

The service role is not an AWS managed role but is created initially for pipeline creation, and then as new permissions are added to the service role policy, you may need to update the service role for your pipeline\. Once your pipeline is created with a service role, you cannot apply a different service role to that pipeline\. Attach the recommended policy to the service role\.

For more information about the service role, see [Manage the CodePipeline service role](security-iam.md#how-to-custom-role)\.