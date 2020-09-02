## Create





`aws ssm get-parameters --names /aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2 --region us-east-1`




### Application Load Balancer (ALB)

* Port 80 listener
* Security Group allowing incoming traffic in the port 80 from anywhere (0.0.0.0/0)
* Healthcheck port 80 path /


### Autoscaling / Launch Configuration / Ec2

*  Use the Amazon Linux 2 ami for your specified region.
*  Desired instance size = 2m max instances 3
*  Add 1 instance when CPU reach more than 80%
*  Remove 1 instance when CPU less than 20%
*  EC2 port 80 access open only from the Load Balancer
*  EC2 port 22 access from anywhere (0.0.0.0/0)

