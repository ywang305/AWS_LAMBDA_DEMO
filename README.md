## About the repo
This repo probes the AWS LAMBDA serverless with JAVA and Nodejs


## Basic tasks

* CloudFormation, AWS SAM CLI, 
SAM uses CloudFormation, an AWS service for managing infrastructure as code. [SAM developer guide](https://docs.aws.amazon.com/serverless-application-model/index.html)

### Create 

#### Deploy SAM application
- sam build

  SAM tools know how to install and bundle dependencies for many common package managers. e.g. NPM, PIP,...
  For compiled languages, such as Java and Go, SAM knows how to turn source into executable code.
  It knows how to ignore test code and resources and avoid bundling development dependencies. This means that you can safely install development tools in your source directory; SA0 will ignore them when building the functions.

- sam package

  to bundle all the file required by each function into separate ZIP archives and upload the results to S3
  
  ```bash
  aws s3 mb s3://BUCKET-NAME. # create a s3
  ```
  SAM has a convenient shortcut to zip up and upload function packages to S3, remember to use your bucket name:
  ```
  sam package --s3-bucket sam-project-deployment --output-template-file output.yaml
  ```

- sam deploy --guided

#### inspect from cli
```
aws cloudformation describe-stacks --stack-name sam-test-1
```

#### log
```bash 
sam logs -n HelloWorldFunction --stack-name sam-test-1
```

#### simulating local

this should start up a local API Gateway emulation and a local Lambda execution environment.

``` 
sam local start-api 
```

#### debugging
  - plugin: AWS-toolkit
  - vscode debugger:  support JS, TS, JAVA, ...
  - click 'AWS: ADD Debug Configuration' at specific handler
  

----

## Working with AWS

- cheaper lambda and how to use it
  
  Having a Lambda function sitting between a user device and S3 is not really useful if it only performs autho- risation. S3 can do that itself. here’s no need to suffer through the additional latency of API proxying and Lambda execution. 
  
  AWS provides several ways of temporarily granting clients the right to do very operations:
  • Wecould let clients usethe AWSSDK directly,and setup IAM for each client.
  • Wecould setup templated IAM policies for groups of end users authenticated with Amazon Cognito, a managed service for user credentials.
  • Wecould usea Lambda function to create temporary grants for clients,so they can access our AWS resources in a limited way.


