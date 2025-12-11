# AWS-Public-Private-Deployment
## Objective 
The of the objective of this project is to gain the needed skills to deploy , manage and troubleshoot VPC's ,Subnet(Both PUBLIC and PRIVATE ) ,Internet Gateway (IGW) , NAT Gataway,Route tables and how they come together to create real life cloud IT architecture and Infrastructure.    

## Steps To Build 
This project was broken into different phase , and the steps taken in each of these phase will be explain in detail .
### Phase 1: AWS VPC With Public Subnet and Internet Gateway 
#### Architecture Diagram For Phase 1
![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(76).png)
 
  Image 01.
  
  Note: The architecture diagram will be changing as I move from one phase to another , Since things will be added as I move.

The following are the steps for this phase:
#### Step 1:
Create The VPC with:
-name: my-1st-vpc 
-IPv4 CIDR : 10.0.0.0/16 , as shown in the image below :
![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(63).png)
   
   Image 02.

The reminding Setting were left on default as shown in the image below :
   ![Alt aws](https://github.com/Adegbenga-111/AWSPublic-Private-Deployment/blob/main/Screenshot%20(64).png)

   Image 03.
#### Step 2:
Create a public Subnet in the VPC with :
-name: Public-Subnet-Phase1
-CIDR : 10.0.1.0/24 .
The summary of the configure in the subnet is shown in the Image below:
  ![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(70).png)


  Image 04.

#### Step 3:
Creating and Attaching an Internet Gateway (IGW)  with name: Phase1-IGW; and the IGW is attached to the VPC created at the start of this project. The reason why IGW is important in this setup ,is because it is the DOOR that connent's the VPC to the internet.    
    ![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(74).png)
    
   Image 05: Creation of the IGW.
   
   ![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(75).png) 
     
   Image 06: Attaching the IGW to the VPC.

#### Step 4:
Creating a Route Table for the Public Subnet , with
  -name : Public-RT-Phase1 
  as shown in the image below :
![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(78).png)

  Image 07.

  After creating the route table , I added a route with :
           -Destination: 0.0.0.0/0 ( The internet)
           -Target : IGW 
  As shown in the image below :
  
  ![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(79).png)

   Image 09.

Than, I have to Associate the route table with the Public Subnet in the page shown in the image below :

![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(80).png)

   Image 09.

#### Step 5: 
Launching an EC2 in the public subnet in the VPC we created , as shown in the image shown below:

![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(86).png)

   Image 10.
   
The specs of the EC2 are as follows :
- OS -> Ubuntu
- Instance type -> t3.micro
- Public IP -> Enable
- Security Group -> allow ssh from anywhere is my ip change.

#### Test 
I conneted to the EC2 instance, then I updated and upgraded the OS run on the VM . As shown in the images below.

 ![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(92).png)
 
   Image 11 : Update.
   
![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(95).png)

Image 12 : After the update was done.

![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(95).png)

Image 13: Through the upgrade.

After this i ran a ping commmand as shown in the image below :

![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(98).png)

Image 14.


As shown in the image above , the EC2 was receiving reply from google sever , which means that phase 1 was a SUCCESS.


### Phase 2: Add Private Subnet + NAT Gateway + Private Route Table + Private EC2

#### Architecture Diagram For Phase 
![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(99).png)

Image 15 

The steps are the continuation of the following steps in the first phase .

#### Step 6 : Creating a private subnet with the following configuration :
 - VPC -> my-1st-vpc
 - Name -> Private-Subnet
 - CIDR -> 10.0.2.0/24
 - and  I did not enable public IP Assignment
All of these above was done in the image below:
![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(100).png)

   Image 16.

![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(101).png)

Image 17: Summary of the setting done in the creation of the subnet.

#### step 7 : Creating a NAT Gataway in the Public Subnet.
The reason for this , as shown in the architecture design , is to enable connection between the EC2 in the public subnet to connect to the EC2 in the  Private subnet .

![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(104).png)

Image 18 .

The image above shows the name of the NAT gate way , the VPC it under and other basic configuration done in the creation of the NAT gateway.

#### Step 8 : Creating a Route Table That is Associate to the Private Subnet.
Creating the route table with the following settings :
-Name:Private-RT
-VPC : my-1st-vpc
 As shown in the image below :
 ![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(105).png)

   Image 19.
Adding new route to the route table with: 
-Destination : 0.0.0.0/0
- Target : NAT gateway (my-NAT-GW)
  ![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(106).png)


 




