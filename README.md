# Udacity-DevOps-Nano-Degree-Deploying High Available WebApp Using CloudFormation

## Scenario

The company is creating an Instagram clone called Udagram.

Developers want to deploy a new application to the AWS infrastructure.

We have been tasked with provisioning the required infrastructure and deploying a dummy application, along with the necessary supporting software.

This needs to be automated so that the infrastructure can be discarded as soon as the testing team finishes their tests and gathers their results.


## Server specs

We'll need to create a Launch Configuration for our application servers in order to deploy four servers, two located in each of our private subnets. The launch configuration will be used by an auto-scaling group.
We'll need two vCPUs and at least 4GB of RAM. The Operating System to be used is Ubuntu 18. 
The desk space allocation should be at least 10GB. 


## Security Groups and Roles


- Udagram communicates on the default HTTP Port: 80, so your servers will need this inbound port open since you will use it with the Load Balancer and the Load Balancer Health Check. As for outbound, the servers will need unrestricted internet access to be able to download and update their software.
- The load balancer allows all public traffic (0.0.0.0/0) on port 80 inbound, which is the default HTTP port. Outbound, it will only be using port 80 to reach the internal servers.
- The application needs to be deployed into private subnets with a Load Balancer located in a public subnet.
- One of the output exports of the CloudFormation script should be the public URL of the LoadBalancer. Bonus points if you add http:// in front of the load balancer DNS Name in the output, for convenience.

-----

## Project Diagram


![Udacity Project2 Diagram](https://user-images.githubusercontent.com/3264417/213655542-e113ead7-08db-461e-bb6b-c751ab398159.jpeg)

-----

# Project Files

### 1. project2.yml

the file contains a script to create the required resources for the project 

**Infra Structure Resources for high availability**
- One VPC
- One Internet Gateway
- Two public Subnet
- Two private Subnets
- Two NatGateway
- Required Route tables for the subnets
- Security Groups for the created subnet


**Servers and assets deployed in the infrastructure**

- Load Balancer
- Autoscalling group
- Launch Configuration for the instances that will be created - with user data to install apache server on it
- Target Group 

### 2. Project2.json

The file contains the required Paramater to run the YAML template file

**EnvironmentName:** 

    Description: it is the environment name
    Type: String

**MyVPCCidrBlockRange:**

    Description: it is the ip range of VPC cidrBlock
    Type: String

**MyPrivateSubnet1CidrBlockRange:**

    Description: it is the ip range of private subnet 1
    Type: String

**MyPrivateSubnet2CidrBlockRange:**

    Description: it is the ip range of private subnet 2
    Type: String

**MyPublicSubnet1CidrBlockRange:**

    Description: it is the ip range of public subnet 1
    Type: String

** MyPublicSubnet2CidrBlockRange:**

    Description: it is the ip range of public subnet 2
    Type: String
    
    
### 3. create.sh

The file is used to run the script of creating cloudformation stack, you should pass 3 values as parameters 
1. stack name
2. template file
3. parameters file

````
  ./create.sh stack_name ./project2.yml ./project2.json

````

### 4. update.sh

The file is used to update the existing stack on the cloudformation and also recieve 3 paramaters as the creat.sh file


--------------------------------
## Outputs

1. After running the project.yml, you will find the DNS URL as an output of the stack as follows:

![image](https://user-images.githubusercontent.com/3264417/213684282-00f8862c-0ae7-4fc6-b2ff-b1cdf5d98d34.png)


2. After navigating to the Load Balancer DNS, the index file will be displayed as follows:

![image](https://user-images.githubusercontent.com/3264417/213684623-99ad0973-b395-4a4f-86de-1c07277e22a1.png)



# Thank You



