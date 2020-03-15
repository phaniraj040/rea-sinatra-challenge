## REA-Sinatra-Challenge
This Repository is for REA Group Coding Challenge

## Provision a configuration-as-code recipe for Simple Sinatra Application Deployment

# Pre-requisites:

Any AWS Ubuntu AMI
e.g ami-02a599eb01e3b3c5b

# Design:
Used a base Ubuntu Image and install ruby dependencies required to run the Sinatra application. Reason to choose a Ubuntu image is for the ease of installing the ruby bundler

Make changes to the sinatra-params.json file by passing the correct values before running the stack creation

# How to run AWS CloudFormation
```
aws cloudformation create-stack --stack-name stack-name --template-body file://sinatra-cfn.yml --parameters file://sinatra-params.json --region ap-southeast-2
```

Once the stack is created, the Sinatra application can be accessed from the LoadBalancer DNS which is available in the Output section.

Example:
http://xxxxxx.ap-southeast-2.elb.amazonaws.com

The application is fully secured, highly available and locked  and only accessible using the LoadBalancer DNS and the SSH access is available only from the Machine IP address provided in the parameters.

Note: packer-sinatra.json is provided if there is a need to bake the AMI with Sinatra applicaion on it and all the dependencies installed
To make use of packer the machine needs to have Packer installed on it and with AWS Credentials to create an AMI. AMI can be created as below
```
packer build -var 'aws_access_key=YOUR ACCESS KEY' -var 'aws_secret_key=YOUR SECRET KEY' packer-sinatra.json
```
