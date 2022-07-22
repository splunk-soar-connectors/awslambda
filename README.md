[comment]: # "Auto-generated SOAR connector documentation"
# AWS Lambda

Publisher: Splunk  
Connector Version: 2\.2\.9  
Product Vendor: AWS  
Product Name: Lambda  
Product Version Supported (regex): "\.\*"  
Minimum Product Version: 5\.2\.0  

This app integrates with AWS Lambda to perform lambda functions

### Configuration Variables
The below configuration variables are required for this Connector to operate.  These variables are specified when configuring a Lambda asset in SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**access\_key** |  optional  | password | Access Key
**secret\_key** |  optional  | password | Secret Key
**region** |  required  | string | Default Region
**use\_role** |  optional  | boolean | Use attached role when running Phantom in EC2

### Supported Actions  
[test connectivity](#action-test-connectivity) - Validate the asset configuration for connectivity using supplied configuration  
[remove permission](#action-remove-permission) - Revokes function\-use permission from an AWS service or another account  
[invoke lambda](#action-invoke-lambda) - Invoke an AWS Lambda function  
[list functions](#action-list-functions) - List available AWS Lambda functions, with the version\-specific configuration for each  
[add permission](#action-add-permission) - Grants an AWS service or another account permission to use a function  

## action: 'test connectivity'
Validate the asset configuration for connectivity using supplied configuration

Type: **test**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
No Output  

## action: 'remove permission'
Revokes function\-use permission from an AWS service or another account

Type: **correct**  
Read only: **False**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**function\_name** |  required  | The name of the Lambda function, version, or alias\. The following name formats are accepted\: function name, function ARN, and partial ARN | string |  `lambda function name`  `lambda function arn` 
**statement\_id** |  required  | Statement identifier of the permission to remove | string | 
**qualifier** |  optional  | Specify a version or alias to remove permissions to a published version of the function | string | 
**revision\_id** |  optional  | Only update the policy if the revision ID matches the ID that's specified\. Use this option to avoid modifying a function policy that has changed since you last read it | string | 
**credentials** |  optional  | Assumed role credentials | string |  `aws credentials` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.data\.\*\.ResponseMetadata\.RequestId | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.date | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.connection | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.content\-type | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.x\-amzn\-requestid | string | 
action\_result\.data\.\*\.ResponseMetadata\.RetryAttempts | numeric | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPStatusCode | numeric | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.status | string | 
action\_result\.parameter\.function\_name | string |  `lambda function name`  `lambda function arn` 
action\_result\.parameter\.statement\_id | string | 
action\_result\.parameter\.qualifier | string | 
action\_result\.parameter\.revision\_id | string | 
action\_result\.parameter\.credentials | string |  `aws credentials` 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'invoke lambda'
Invoke an AWS Lambda function

Type: **generic**  
Read only: **False**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**function\_name** |  required  | The name of the AWS Lambda function, version, or alias\. The following name formats are accepted\: function name, function ARN, and partial ARN | string |  `lambda function name`  `lambda function arn` 
**invocation\_type** |  optional  | Invocation type | string | 
**log\_type** |  optional  | Set to 'Tail' to include the execution log in the response | string | 
**client\_context** |  optional  | The JSON that you want to provide to your Lambda function in the context object | string | 
**payload** |  optional  | The JSON that you want to provide to your Lambda function as input | string | 
**qualifier** |  optional  | Specify a version or alias to invoke a published version of the function | string | 
**credentials** |  optional  | Assumed role credentials | string |  `aws credentials` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.client\_context | string | 
action\_result\.parameter\.credentials | string |  `aws credentials` 
action\_result\.parameter\.function\_name | string |  `lambda function name`  `lambda function arn` 
action\_result\.parameter\.invocation\_type | string | 
action\_result\.parameter\.log\_type | string | 
action\_result\.parameter\.payload | string | 
action\_result\.parameter\.qualifier | string | 
action\_result\.data\.\*\.ExecutedVersion | string | 
action\_result\.data\.\*\.FunctionError | string | 
action\_result\.data\.\*\.Payload | string | 
action\_result\.data\.\*\.Payload\.errorMessage | string | 
action\_result\.data\.\*\.Payload\.errorType | string | 
action\_result\.data\.\*\.Payload\.stackTrace\.\* | string | 
action\_result\.data\.\*\.Payload\.statusCode | numeric | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.connection | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.content\-length | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.content\-type | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.date | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.x\-amz\-executed\-version | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.x\-amz\-function\-error | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.x\-amzn\-remapped\-content\-length | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.x\-amzn\-requestid | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.x\-amzn\-trace\-id | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPStatusCode | numeric | 
action\_result\.data\.\*\.ResponseMetadata\.RequestId | string | 
action\_result\.data\.\*\.ResponseMetadata\.RetryAttempts | numeric | 
action\_result\.data\.\*\.StatusCode | numeric | 
action\_result\.summary\.status | string | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'list functions'
List available AWS Lambda functions, with the version\-specific configuration for each

Type: **investigate**  
Read only: **True**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**function\_version** |  optional  | Set to 'ALL' to include entries for all published versions of each function | string | 
**next\_token** |  optional  | Specify the pagination token returned by previous request to retrieve next page of results | string |  `lambda next token` 
**max\_items** |  optional  | A value between 1 and 50 to limit the number of functions to be returned | numeric | 
**credentials** |  optional  | Assumed role credentials | string |  `aws credentials` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.credentials | string |  `aws credentials` 
action\_result\.parameter\.function\_version | string | 
action\_result\.parameter\.max\_items | numeric | 
action\_result\.parameter\.next\_token | string |  `lambda next token` 
action\_result\.data\.\*\.Functions\.\*\.CodeSha256 | string | 
action\_result\.data\.\*\.Functions\.\*\.CodeSize | numeric | 
action\_result\.data\.\*\.Functions\.\*\.Description | string | 
action\_result\.data\.\*\.Functions\.\*\.FunctionArn | string |  `lambda function arn` 
action\_result\.data\.\*\.Functions\.\*\.FunctionName | string |  `lambda function name` 
action\_result\.data\.\*\.Functions\.\*\.Handler | string | 
action\_result\.data\.\*\.Functions\.\*\.LastModified | string | 
action\_result\.data\.\*\.Functions\.\*\.MemorySize | numeric | 
action\_result\.data\.\*\.Functions\.\*\.RevisionId | string | 
action\_result\.data\.\*\.Functions\.\*\.Role | string | 
action\_result\.data\.\*\.Functions\.\*\.Runtime | string | 
action\_result\.data\.\*\.Functions\.\*\.Timeout | numeric | 
action\_result\.data\.\*\.Functions\.\*\.TracingConfig\.Mode | string | 
action\_result\.data\.\*\.Functions\.\*\.Version | string | 
action\_result\.data\.\*\.Functions\.\*\.VpcConfig\.VpcId | string | 
action\_result\.data\.\*\.NextMarker | string |  `lambda next token` 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.connection | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.content\-length | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.content\-type | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.date | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.x\-amzn\-requestid | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPStatusCode | numeric | 
action\_result\.data\.\*\.ResponseMetadata\.RequestId | string | 
action\_result\.data\.\*\.ResponseMetadata\.RetryAttempts | numeric | 
action\_result\.summary\.next\_token | string |  `lambda next token` 
action\_result\.summary\.num\_functions | numeric | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric |   

## action: 'add permission'
Grants an AWS service or another account permission to use a function

Type: **generic**  
Read only: **False**

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**function\_name** |  required  | The name of the Lambda function, version, or alias\. The following name formats are accepted\: function name, function ARN, and partial ARN | string |  `lambda function name`  `lambda function arn` 
**statement\_id** |  required  | A statement identifier that differentiates the statement from others in the same policy | string | 
**action** |  required  | The action that the principal can use on the function\. For example, lambda\:InvokeFunction or lambda\:GetFunction | string | 
**principal** |  required  | The AWS service or account that invokes the function\. If you specify a service, use SourceArn or SourceAccount to limit who can invoke the function through that service | string | 
**source\_arn** |  optional  | For AWS services, the ARN of the AWS resource that invokes the function\. For example, an Amazon S3 bucket or Amazon SNS topic | string | 
**source\_account** |  optional  | For AWS services, the ID of the account that owns the resource\. Use this instead of SourceArn to grant permission to resources that are owned by another account \(for example, all of an account's Amazon S3 buckets\)\. Or use it together with SourceArn to ensure that the resource is owned by the specified account\. For example, an Amazon S3 bucket could be deleted by its owner and recreated by another account | string | 
**event\_source\_token** |  optional  | For Alexa Smart Home functions, a token that must be supplied by the invoker | string | 
**qualifier** |  optional  | Specify a version or alias to add permissions to a published version of the function | string | 
**revision\_id** |  optional  | Only accepts the function's $LATEST revision ID\. Use this option to avoid modifying a function policy that has changed since you last read it | string | 
**credentials** |  optional  | Assumed role credentials | string |  `aws credentials` 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.status | string | 
action\_result\.parameter\.action | string | 
action\_result\.parameter\.credentials | string |  `aws credentials` 
action\_result\.parameter\.event\_source\_token | string | 
action\_result\.parameter\.function\_name | string |  `lambda function name`  `lambda function arn` 
action\_result\.parameter\.principal | string | 
action\_result\.parameter\.qualifier | string | 
action\_result\.parameter\.revision\_id | string | 
action\_result\.parameter\.source\_account | string | 
action\_result\.parameter\.source\_arn | string | 
action\_result\.parameter\.statement\_id | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.connection | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.content\-length | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.content\-type | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.date | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPHeaders\.x\-amzn\-requestid | string | 
action\_result\.data\.\*\.ResponseMetadata\.HTTPStatusCode | numeric | 
action\_result\.data\.\*\.ResponseMetadata\.RequestId | string | 
action\_result\.data\.\*\.ResponseMetadata\.RetryAttempts | numeric | 
action\_result\.data\.\*\.Statement | string | 
action\_result\.summary\.status | string | 
action\_result\.message | string | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric | 