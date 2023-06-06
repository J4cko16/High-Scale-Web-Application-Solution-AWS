# High-Scale-Web-Application-Solution-AWS
An AWS Solution for a highly scalable low latency web application.

# Senario
Example University is preparing for the new school year. The admissions department has received complaints that their web application for student records is slow or not available during the peak admissions period because of the high number of inquiries.

You are a cloud engineer. Your manager has asked you to create a proof of concept (POC) to host the web application in the AWS Cloud. Your manager would like you to design and implement a new hosting architecture that will improve the experience for users of the web application. You’re responsible for building the infrastructure to host the student records web application in the cloud.

Your challenge is to plan, design, build, and deploy the web application to the AWS Cloud in a way that is consistent with best practices of the AWS Well-Architected Framework. During the peak admissions period, the application must support thousands of users, and be highly available, scalable, load balanced, secure, and high performing.

# Step 1 (Creating a Virtual Machine):
A basic VPC and security group were already created when I booted my AWS service. So I needed a virutal matchine to host the web application. Using AmazonEC2 I assigned a public IPv4 address to the Virtual Machine. The AMI I used was the latest free Ubuntu2023 AMI that they allowed since Ubuntu is a powerful version of Linux that could handle lots of data at once in order to hold all of the data required for the student regestration and since Linux is able to run bash which is a form of scripiting that I will be using. Then I selected the basic security group given to me for the time being and also selected my premade VPC since it met the requirements of what I wanted to use it for. There is a website I wanted to link to the EC2 so I used a bash script given to me for the senario since it works with Linux computers. The EC2 was made but you can't go onto the web application since there is no path so I created an inbound rule in the security group using a "Any IPv4" route and with a TCP protocol. Using TCP allows for slower but better web traffic control and the Any IPv4 allows for my EC2's Ipv4 to work as the website link allowing me to load the web application as shown in the image below.

![step 1 1](https://github.com/J4cko16/High-Scale-Web-Application-Solution-AWS/assets/102924228/a7ff5ae5-0b54-461f-b1d3-d21b1212918a)

![step 1 2](https://github.com/J4cko16/High-Scale-Web-Application-Solution-AWS/assets/102924228/7349a6e7-021b-4144-aea6-1ca443d2bebe)

# Step 2 (Creating an Application Load Balencer):
Load Balencers scale your load capacity automatically in response to changes in incoming traffic on your web server. I made a load balencer using the AWS EC2 service and gave it my default VPC and Security Group since they're the only ones I currently have access to. I allowed it to access to 6 availability zones all under the us-east subnets in order to make anyone in the east have fast connection to this web application. For the listener of the Load Balencer I gave it a protocol for HTTP:80 which checks for connection requests on its port and protocol. The listener receives traffic and routes it according to its rules allowing me to make custom rules for the website traffic.

![step 2 1](https://github.com/J4cko16/High-Scale-Web-Application-Solution-AWS/assets/102924228/5b8c930e-a87f-41ba-87d5-63fdc800c21b)

![step 2 2](https://github.com/J4cko16/High-Scale-Web-Application-Solution-AWS/assets/102924228/27286c5a-a8cf-4dd0-9030-152c2a10e6df)

# Step 3 (Creating an Auto Scaling Group): 
Using Amazon EC2 I created an auto scaling group. The auto scaling group creates or removes instances based on how strong the load is on your webservers CPU. My auto scaling group goes based on a unit scale and I have the minimum strength at 1 unit and the max at 300. My desired capacity is 4 units. With my desired capacity at 4 units it allows for a semi-strong web application at all times and can change based on the load to up to 300 units. I have no minimum or maximum on my instance type requirements allowing for any of my instances to be scaled very high. I have a health check that checks for EC2 and ELB with a grace period of 300 making sure the only instances that are working are running and terminating any instances that are unused or not working.

![step 3 1](https://github.com/J4cko16/High-Scale-Web-Application-Solution-AWS/assets/102924228/aeebf252-c686-48d5-bee2-bf3579604fd5)

# Step 4 (Creating a Load Test):
I created a load test in order to test how my highly scalable web application adjusts with a heavy traffic flow. I first started by using AWS Cloud9. Cloud9 allows for write, run, and debug for my code with just a browser and also has direct connection to my AWS instances making it very quick to start using instead of installing alternate software and having to use a key and my public IPv4 to log-in to my console. Once loaded into Cloud9 I created an enviroment that is an EC2 instance with a t2.micro instance type using Ubuntu. Creating a new EC2 with my enviroment and on a Linux allows for very easy command prompt use. Creating a brand new EC2 allows me to have a single computer be responsible for running the load test and nothing else. Once the enviroment is created I use the enviroment by hitting "connect" then once in the terminal I install a load test software onto the computer in order to be able to run the load test since it is not installed at the start. Once the load test is installed I run the test to my VPC cpu since is directly linked to  the EC2. The test simulates around 5,000 users going onto the website. This represents how much the load will be when kids are signing up for the college. The test was successful with over 30 load balencers being created showing that it balenced to the load required.

![step 4 1](https://github.com/J4cko16/High-Scale-Web-Application-Solution-AWS/assets/102924228/e6c56b2e-0581-4a25-900f-f1d09bceb3d4)

![step 4 2](https://github.com/J4cko16/High-Scale-Web-Application-Solution-AWS/assets/102924228/0e34bc03-5567-4853-ac05-b9cc30db052a)

# Step 5 (Finishing Up):
Once everything was done I documented all of my steps that I have done and took pictures of important parts of the project. Then researched how to add them to this file.

# Lucid Chart Plan (Beginning vs End):
 # Beginning:
![step 6 1](https://github.com/J4cko16/High-Scale-Web-Application-Solution-AWS/assets/102924228/87d550a8-1f5b-4a35-869e-24e690c1b26e)
<br> I had no clue what I was doing at the beginning of this project. If it doesn't make sense to you that is because I had no clue what I was doing at first. I have come a long way since starting this project.
# End:
<img width="949" alt="Screen Shot 2023-06-05 at 9 21 39 PM" src="https://github.com/J4cko16/High-Scale-Web-Application-Solution-AWS/assets/102924228/3f7c0f4a-da2c-4504-b7de-9a71998faca8">
<br> First of all the user types in the public IPv4 in the search bar. Once the IPv4 is typed it will direct to the security groups inbound rule and call the HTTP any IPv4 protocol. Once the protocol is called the user has access to the IPv4 domain of the EC2 and logs on the the web application being hosted by the EC2's bash script. Meanwhile while the EC2 instance is active the load balencing is always checking the load of the server and is constantly changing the traffic of the server to mutliple availability zones in order to balence the traffics load to make the website as latency free as possible. Then the auto scaling group is responding to the inbalence in load and scanning it using a health check every 300 seconds. Once the health check has been completed it gives the auto scaling a signal of the load that is currently needed and adjusts or adds the instances accordingly by terminating uneeded instances or adding new ones to help with the sudden traffic. While all of this is happening the VPC is the base of it all. The VPC is pretty much just the virutal cloud enviroment and the EC2 services are all linking to it in order to host the web application. With this solution the user should be able to enoy a nice auto scaling web application without any or much latency.
