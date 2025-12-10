# AWS-Public-Private-Deployment
## Objective 
The of the objective of this project is to gain the needed skills to deploy , manage and troubleshoot VPC's ,Subnet(Both PUBLIC and PRIVATE ) ,Internet Gateway (IGW) , NAT Gataway,Route tables and how they come together to create real life cloud IT architecture and Infrastructure.    
## Architecture Diagram 
The image below gives an overview of how each component comes together to make this deployment possible.


## Steps To Build 
This project was broken into different phase , and the steps taken in each of these phase will be explain in detail .
### Phase 1: AWS VPC With Public Subnet and Internet Gateway 
#### Architecture Diagram For Phase 1
![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(76).png)
 
  Image 02.
  
  Note: The architecture diagram will be changing as I move from one phase to another , Since things will be added as I move.

The following are the steps for this phase:
#### Step 1:
Create The VPC with:
-name: my-1st-vpc 
-IPv4 CIDR : 10.0.0.0/16 , as shown in the image below :
![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(63).png)
   
   Image 3.

The reminding Setting were left on default as shown in the image below :
   ![Alt aws](https://github.com/Adegbenga-111/AWSPublic-Private-Deployment/blob/main/Screenshot%20(64).png)

   Image 4.
#### Step 2:
Create a public Subnet in the VPC with :
-name: Public-Subnet-Phase1
-CIDR : 10.0.1.0/24 .
The summary of the configure in the subnet is shown in the Image below:
  ![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(70).png)


  Image 5.

#### Step 3:
Creating and Attaching an Internet Gateway (IGW)  with name: Phase1-IGW; and the IGW is attached to the VPC created at the start of this project. The reason why IGW is important in this setup ,is because it is the DOOR that connent's the VPC to the internet.    
    ![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(74).png)
    
   Image 6: Creation of the IGW.
   
   ![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(75).png) 
     
   Image 7 : Attaching the IGW to the VPC.

#### Step 4:
Creating a Route Table for the Public Subnet , with
  -name : Public-RT-Phase1 
  as shown in the image below :
![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(78).png)

  Image 8.

  After creating the route table , I added a route with :
           -Destination: 0.0.0.0/0 ( The internet)
           -Target : IGW 
  As shown in the image below :
  
  ![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(79).png)

   Image 9.

Than, I have to Associate the route table with the Public Subnet in the page shown in the image below :

![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(80).png)

   Image 10.

#### Step 5: 
Launching an EC2 in the public subnet in the VPC we created , as shown in the image shown below:

![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(86).png)

   Image 11.
   
The specs of the EC2 are as follows :
- OS -> Ubuntu
- Instance type -> t3.micro
- Public IP -> Enable
- Security Group -> allow ssh from anywhere is my ip change.

#### Test 
I conneted to the EC2 instance, then I updated and upgraded the OS run on the VM . As shown in the images below.

 ![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(92).png)
 
   Image 12 : Update.
   
![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(95).png)

Image 13 : After the update was done.

![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(95).png)

Image 14: Through the upgrade.

After this i ran a ping commmand as shown in the image below :

![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(98).png)

Image 15.


As shown in the image above , the EC2 was receiving reply from google sever , which means that phase 1 was a SUCCESS.
