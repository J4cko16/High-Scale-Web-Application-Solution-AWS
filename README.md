# High-Scale-Web-Application-Solution-AWS
An AWS Solution for a highly scalable low latency web application.

# Step 1 (Creating a Virtual Machine):
A basic VPC and security group were already created when I booted my AWS service. So I needed a virutal matchine to host the web application. Using AmazonEC2 I assigned a public IPv4 address to the Virtual Machine. The AMI I used was the latest free Ubuntu2023 AMI that they allowed. Then after choosing the AMI I selected the basic security group given to me for the time being and also selected my premade VPC since it met the requirements of what I wanted to use it for. There is a website I wanted to link to the EC2 so I used a standard bash script to achieve this. The EC2 was made but you can't go onto the web application since there is no path so I created an inbound rule in the security group using a "Any IPv4" route and with a TCP protocol. The inbound rule you can successfully go to the web application!

# Step 2 (Creating an Application Load Balencer):
Load Balencers scale your load capacity automatically in response to changes in incoming traffic on your web server. I made a load balencer using the AWS EC2 service and gave it my default VPC and Security Group. I allowed it to access to 6 availability zones all under the us-east subnets in order to make anyone in the east have fast connection to this web application. For the listener of the Load Balencer I gave it a protocol for HTTP:80 which checks for connection requests on its port and protocol. The listener receives traffic and routes it according to its rules.

