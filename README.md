         ___        ______     ____ _                 _  ___  
        / \ \      / / ___|   / ___| | ___  _   _  __| |/ _ \ 
       / _ \ \ /\ / /\___ \  | |   | |/ _ \| | | |/ _` | (_) |
      / ___ \ V  V /  ___) | | |___| | (_) | |_| | (_| |\__, |
     /_/   \_\_/\_/  |____/   \____|_|\___/ \__,_|\__,_|  /_/ 
 ----------------------------------------------------------------- 
Question
Please write an Ansible role(s) that does the following:

Create a VPC and Implement Security Best practice (Look into it )
Create a Security Group (on the newly created VPC) which only allows access from the following: 
Inbound - Your IP address (SSH, HTTP); Ansible IP address (SSH)
Outbound – HTTPS & HTTP to any IP address
Launches a Linux instance from an AMI (select t2.micro for type of instance) and assign it with the Security Group that you created in (2). 
You can select which flavor of Linux to launch.  --> RHEL 7  / Ubuntu 
Add a tag EnvName with the value “Test Environment”


Deploy a Linux web-application (you can choose a web-application that you like) to the instance that you provisioned.
Present a web-page that is showing the IP address of the local IP address of machine on which it is running and have the web-app to listen on port 80


Setting up a new VPC with both public and private subnets.
Implementing a NAT Gateway to ensure instances in the private subnet can access the internet.
Setting up an Application Load Balancer (ALB) in front of EC2 instances for high availability.
Using Hashicorp Vault for sensitive data.
Autoscaling groups for fault tolerance and scalability.
Expectations:
Upload to Github and share link with me 
Create a Blog/Documentation outlining step-by-step procedure and be ready to explain to me on Friday  

Solution.
This project involves the use of ansible role  as IaC (Infrastructure as Code) and configuration management tool. In thgis project, ansible was used to set up an EC2 server. This involves 
creating a VPC, Cidr blocks, Subnets, Internet gateways, and Route Tables using Ansible. Web application was later deployed into this instance with Ansible.

Stages
1. Install necessary dependencies:
     To use ansible, there are some required depencies that ansible will need to operate efficiently. These are:
      a. Python3
      b. Python3-pip
      c. Configure aws - set up both AWS Access keys and Secret Keys using aws configure
      d. Boto3 and botocore
2. Install Ansible:
   Though AWS server can be used to set up our environment, for this project, I used visual studio code (VScode) as my ide to provision my server (All references will be made towards using VScode
   as provisioning ide). Then ansible was installed with ansible galaxy collection and ansible vaults as illustrated below:
     a. Sudo apt-get install ansible
     b. ansible-galaxy collection install amazon.aws
     c. ansible-vault create myvault.yml
3. Environment Setup:
    Since I am using ansible roles to deploy and patch my servers, I initially created my main folder (ansible project) and added a roles folder as a subdirectory to this. In the roles subdirectory,
    I divided my activities into stages as shown below:
               vpc --> sg --> webserver --> deployment
       a. vpc stage:
         This stage involves the creation of Virtual Private Cloud (VPC as network isolation). Subnets, Internet gateway, route table reaources were also designed to communicate with one and create
         an internet gateway to the instance that will be eventually created.
       b. sg stage:
         The next stage designed was the security group (sg). This provides neccessary isolation to the resources at instance level. In this project, ports 22 (to allow ssh), port 80 (http) and port 443 (https)
         were allowed for imboud rule while outbound was left open to all traffic.
       c. webserver stage:
          This is where the instance to be spun up was set up. Instance size, required ami image, vpc, subnet among others were deployed to set up the instance in the vpc and subnet mentioned above.
       d. deployment stage:
           In this stage, webapp was deployed to the instance (in runningf stage). httpd was set up and used to patch the server.

   Setting up dynamic Plugin:
   This is to enable ansible to grab the public ip of a newly changed or created instance. The steps to automate this process is listed below:
   1 install "ansible-galaxy collection install amazon.aws"
   2. Create a yaml file that ends with aws_ec2.yml or aws_ec2.yaml (aws_ec2.yml)

   Problems:
   The instance was deployed using ansible but I am still having problem changing the host from localhost (that was used to deploy the instance) to the ec2 so as to patch it.
   
   
