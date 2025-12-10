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
Create The VPC with the name: my-1st-vpc ; and IPv4 CIDR : 10.0.0.0/16 , as shown in the image below :
![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(63).png)
   
   Image 3.

The reminding Setting were left on default as shown in the image below :
   ![Alt aws](https://github.com/Adegbenga-111/AWSPublic-Private-Deployment/blob/main/Screenshot%20(64).png)

   Image 4.
#### Step 2:
Create a public Subnet in the VPC with name: Public-Subnet-Phase1; with CIDR : 10.0.1.0/24 .
The summary of the configure in the subnet is shown in the Image below:
  ![Alt aws](https://github.com/Adegbenga-111/AWS-Public-Private-Deployment/blob/main/Screenshot%20(70).png)



