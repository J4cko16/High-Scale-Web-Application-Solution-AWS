# High-Scale-Web-Application-Solution-AWS
An AWS Solution for a highly scalable low latency web application.

# Step 1 (Creating a Virtual Machine):
A basic VPC and security group were already created when I booted my AWS service. So I needed a virutal matchine to host the web application. Using AmazonEC2 I assigned a public IPv4 address to the Virtual Machine. The AMI I used was the latest free Ubuntu2023 AMI that they allowed. Then after choosing the AMI I selected the basic security group given to me for the time being and also selected my premade VPC since it met the requirements of what I wanted to use it for. There is a website I wanted to link to the EC2 so I used a standard bash script to achieve this. The EC2 was made but you can't go onto the web application since there is no path so I created an inbound rule in the security group using a "Any IPv4" route and with a TCP protocol. The inbound rule you can successfully go to the web application!

# Step 2 (Creating an Application Load Balencer):
Load Balencers scale your load capacity automatically in response to changes in incoming traffic on your web server. I made a load balencer using the AWS EC2 service and gave it my default VPC and Security Group. I allowed it to access to 6 availability zones all under the us-east subnets in order to make anyone in the east have fast connection to this web application. For the listener of the Load Balencer I gave it a protocol for HTTP:80 which checks for connection requests on its port and protocol. The listener receives traffic and routes it according to its rules.

# Step 3 (Creating an Auto Scaling Group): 
Using Amazon EC2 I created an auto scaling group. The auto scaling group creates or removes instances based on how strong the load is on your webservers CPU. My auto scaling group goes based on a unit scale and I have the minimum strength at 1 unit and the max at 300. My desired capacity is 4 units. I have no minimum or maximum on my instance type requirements allowing for any of my instances to be scaled. I have a health check that checks for EC2 and ELB with a grace period of 300 making sure the only instances that are working are running and terminating any instances that are unused or not working.

# Step 4 (Creating a Load Test):
I created a load test in order to test how my highly scalable web application 
