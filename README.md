## REA-Sinatra-Challenge
This Repository is for REA Group Coding Challenge

## Provision a configuration-as-code recipe for Simple Sinatra Application Deployment

# Pre-requisites:
A Machine with Packer installed to build the AMI with all the dependencies installed for deploying the Sinatra Application

AWS IAM User with AWSSecretKey and AWSAccessKeyId

# Design:
Used a base Ubuntu Image and install ruby dependencies required to run the Sinatra application. Reason to choose a Ubuntu image is for the ease of installing the ruby bundler

To build AMI required for our Sinatra application:

# How to Bake an AMI
```
packer build -var 'aws_access_key=YOUR ACCESS KEY' -var 'aws_secret_key=YOUR SECRET KEY' packer-sinatra.json
```

The above command create an AMI in the AWS account.

Use the above baked image to create a Stack in AWS to comply with DevSecOps Principles

Make changes to the sinatra-params.json file by passing the correct values before running the stack creation

# How to run AWS CloudFormation
```
aws cloudformation create-stack --stack-name stack-name --template-body file://sinatra-cfn.yml --parameters file://sinatra-params.json --region ap-southeast-2
```

Once the stack is created, the Sinatra application can be accessed from the LoadBalancer DNS which is available in the Output section.

Example:
http://xxxxxx.ap-southeast-2.elb.amazonaws.com

The application is fully secured, highly available and locked  and only accessible using the LoadBalancer DNS and the SSH access is available only from the Machine IP address provided in the parameters.
