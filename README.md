# AWS Public & Private Network Deployment

## Executive Summary

This project demonstrates the design, deployment, and troubleshooting of a **secure AWS VPC architecture** using public and private subnets. It simulates a real-world cloud environment where public-facing access is tightly controlled and private resources are isolated, while still maintaining outbound internet connectivity.

The project focuses on **AWS networking fundamentals, secure EC2 access patterns, routing, and operational troubleshooting**, aligning closely with Cloud Support and Junior Cloud Engineer responsibilities.

---

## Problem Statement

Organizations require cloud networks that:

* Expose only necessary resources to the internet
* Isolate internal systems from direct public access
* Allow private resources to reach the internet securely
* Support safe administrative access and troubleshooting

This project solves that problem by implementing a **bastion-host-based architecture** with a NAT gateway and least-privilege network controls.

---

## Architecture Overview

### High-Level Design

* Custom VPC with CIDR `10.0.0.0/16`
* One public subnet (bastion host)
* One private subnet (internal workload)
* Internet Gateway for public access
* NAT Gateway for private outbound traffic
* Separate route tables for public and private subnets

### Traffic Flow

* Administrator → Public EC2 (Bastion Host)
* Bastion Host → Private EC2 (SSH)
* Private EC2 → Internet (via NAT Gateway)

### Architecture Diagram

*(See architecture images in the repository for each phase)*

---

## Build Phases

### Phase 1: Public Subnet with Internet Access

**Components Implemented:**

* VPC creation with custom CIDR
* Public subnet (`10.0.1.0/24`)
* Internet Gateway attached to VPC
* Public route table with `0.0.0.0/0 → IGW`
* EC2 instance with public IP for testing connectivity

**Validation:**

* Successful SSH access to public EC2
* Internet reachability confirmed using ICMP (ping)

---

### Phase 2: Private Subnet with Controlled Access

**Components Implemented:**

* Private subnet (`10.0.2.0/24`) with no public IPs
* NAT Gateway deployed in public subnet
* Private route table with `0.0.0.0/0 → NAT Gateway`
* Private EC2 instance with inbound access restricted

**Security Controls:**

* No public IP assigned to private EC2
* SSH access allowed only from bastion host
* Network segmentation enforced using route tables

---

## Security Design

* Bastion host pattern for administrative access
* Private EC2 fully isolated from the internet
* Least-privilege Security Group rules
* No inbound internet traffic to private subnet
* Controlled outbound traffic via NAT Gateway

---

## Incident & Troubleshooting Documentation

### Incident: SSH Access Failure to Private EC2

**Impact:**
Unable to establish SSH connection from bastion host to private EC2.

**Root Cause:**
SSH key pairs required for the private instance were not available on the bastion host.

**Resolution:**

* Installed PuTTY and PuTTY Agent
* Loaded required SSH keys into the agent
* Enabled SSH agent forwarding on the bastion host

**Outcome:**
Successful SSH access to the private EC2 without copying private keys between hosts.

**Prevention:**
Use agent forwarding or AWS Session Manager to avoid key distribution issues.

---

## Validation Tests

* Verified private EC2 outbound internet access via NAT Gateway
* Confirmed no direct inbound access to private EC2 from the internet
* Confirmed controlled SSH access path through bastion host

---

## Detailed Build Documentation
Step-by-step implementation, configuration screenshots, and troubleshooting notes are documented in  
➡️ [`phases.md`](/learning-notes/phase-1.md)


## Lessons Learned

* Proper route table association is critical for subnet behavior
* NAT Gateways enable secure outbound access without exposing private resources
* Bastion hosts reduce attack surface when configured correctly
* SSH access issues are often related to key management rather than networking

---

## Skills Demonstrated

* AWS VPC and subnet design
* Secure EC2 access patterns
* Route table and gateway configuration
* Network isolation and traffic flow control
* Cloud troubleshooting and incident resolution

---

## Future Improvements

* Replace SSH access with AWS Systems Manager Session Manager
* Add Application Load Balancer and Auto Scaling Group
* Introduce database tier in private subnet
* Enable VPC Flow Logs and CloudWatch monitoring

---

*This project reflects a production-style network design and operational mindset suitable for Cloud Support and Junior Cloud Engineer roles.*
