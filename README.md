# CLOUD FORMATION TEMPLATE - INFRA STRUCTURE AS CODE

The project has CloudFormation templates that creates nested stacks for creating :

1. ### A VPC with 2 Public and 2 Private Subnets.
  - Will create a NAT gateway in both public subnets for QA and Production environment for HA.
  - Public and Private Routes
  - Public NACL
  - For Development environment, only one NAT Gateway will be created to keep the cost down.
  - Private Subnets has route to NAT Gateways internet connectivity.
  - Creates VPC flow logs that is pushed into Cloudwatch.
  - Internet Gateway for network connectivity.
2. #### An Application Load Balancer
  - Will have a default target group.
  - Will have a security group allowing HTTP and HTTPS connection from internet.
3. #### A website application with EC2 autoscaling
  - An AutoScaling Group with  a LaunchTemplate.
  - A WebServer target gorup that registers with ALB Listener over HTTP.
  - A scaling policy based on the CPU Usage.
  - A Security group that only allows traffic from loadbalancer.


## Architecture

 ![Architecture](architecture.png)

## Deploy Using UI

First Upload all the ``yaml`` files into a S3 bucket. Update the S3 references to the Infra and application yaml in the master.yml file.

You can go to CloudFormation and create stack. Choose the uploaded S3 ``maser.yaml`` and create the stack. 
