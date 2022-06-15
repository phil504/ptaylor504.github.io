---
layout: default
title: AWS Programmatic Login
parent: AWS Tips
---
<div class="code-example" markdown="1">
```java
try {            
       s3Client = AmazonS3ClientBuilder
        	.standard()
             .withRegion(Regions.US_EAST_1)
             .withCredentials(new DefaultAWSCredentialsProviderChain())
             .build();
        }
```
</div>

When you initialize a new service client without supplying any arguments, the AWS SDK for Java attempts to find AWS credentials by using the default credential provider chain implemented by the DefaultAWSCredentialsProviderChain class. The default credential provider chain looks for credentials in this order:

1.	Environment variables–AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY. The AWS SDK for Java uses the EnvironmentVariableCredentialsProvider class to load these credentials.
2.	Java system properties–aws.accessKeyId and aws.secretKey. The AWS SDK for Java uses the SystemPropertiesCredentialsProvider to load these credentials.
3.	The default credential profiles file– typically located at ~/.aws/credentials (location can vary per platform), and shared by many of the AWS SDKs and by the AWS CLI. The AWS SDK for Java uses the ProfileCredentialsProvider to load these credentials.
You can create a credentials file by using the aws configure command provided by the AWS CLI, or you can create it by editing the file with a text editor. For information about the credentials file format, see AWS Credentials File Format.
4.	Amazon ECS container credentials– loaded from the Amazon ECS if the environment variable AWS_CONTAINER_CREDENTIALS_RELATIVE_URI is set. The AWS SDK for Java uses theContainerCredentialsProvider to load these credentials.
5.	Instance profile credentials– used on EC2 instances, and delivered through the Amazon EC2 metadata service. The AWS SDK for Java uses the InstanceProfileCredentialsProvider to load these credentials.
