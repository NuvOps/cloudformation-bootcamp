
Create a two tier architecture using **Cloud Formation**

AWS Services to create:

* EC2
* Application Load Balancer
* Security Groups
* CloudWatch Alarms
* Autoscaling
* Launch Configuration


## Requirements

### CloudFormation Inputs Parameters

 * AMI ID
 * KeyName (create a key pair manually)
 * VpcId	(use the default VPC for your region)
 * Subnets	(default Subnets, choose at least 2 in different AZs)


### Application Load Balancer (ALB)

* Port 80 listener
* Security Group allowing incoming traffic in the port 80 from anywhere (0.0.0.0/0)
* Healthcheck port 80 path /

### Autoscaling / Launch Configuration / Ec2

*  Use the Latest Amazon Linux 2 ami for your specified region.
   *For example to get the latest Amazon Linux 2 from awscli in the us-east-1 region*:
   `aws ssm get-parameters --names /aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2 --region us-east-1 `
*  Desired instance size = 2m max instances 3
*  Add 1 instance when CPU reach more than 80%
*  Remove 1 instance when CPU less than 20%
*  EC2 port 80 access open only from the Load Balancer
*  EC2 port 22 access from anywhere (0.0.0.0/0)
*  Install apache from userdata
   Example:

   ```bash
      UserData:
        'Fn::Base64': !Sub |
          #!/bin/bash
          yum update -y
          yum install -y httpd
          systemctl start httpd

