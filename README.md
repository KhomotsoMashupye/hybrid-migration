# Hybrid AWS Architecture – Oracle Database On-Prem Integration

> *Architected by:* Khomotso Mashupye  
> *Status:* Complete  
> *Architecture Type:* Hybrid Cloud (AWS + On-Premises)

##  Overview

This project showcases a *hybrid cloud architecture* that securely connects an *on-premises data center* (with Oracle DB and Active Directory) to *AWS infrastructure* using a *Site-to-Site VPN. The AWS side is deployed across **two Availability Zones (AZs)* for high availability and resilience.

The design emphasizes:
- Secure and encrypted data exchange
- Fault-tolerant application hosting in AWS
- Scalable architecture for future growth
- Clear separation of public and private components

##  Architecture Components

###  On-Premises:
- *Customer Gateway (CGW)* – VPN endpoint on-prem
- *VMware Server* – Simulates legacy on-prem workloads
- *Active Directory* – Identity services (e.g., AD Connector/AWS Directory Service ready)
- *Oracle Database* – Core relational data store

### AWS Cloud:
- *Virtual Private Gateway (VGW)* – AWS-side VPN termination
- *VPC* – Spans 2 AZs with:
  - *Public Subnets* – NAT Gateway, Internet Gateway, Load Balancer
  - *Private Subnets* – EC2 instances, Application Tier
- *Internet Gateway (IGW)* – Internet access for public components
- *Application Load Balancer (ALB)* – Cross-AZ traffic distribution
- *NAT Gateways* – Enable private subnet outbound traffic
- *Route Tables* – Handle traffic routing between subnets and gateways

##  Security & Best Practices

- *End-to-End Encryption:*
  - *VPN Tunnel* with IPsec encryption for on-prem to AWS traffic
  - *In-transit encryption (TLS)* for ALB → EC2 communication
  - *At-rest encryption* on EC2 volumes (EBS), S3, and databases (where applicable)
- *IAM Roles & Policies* – Ensure least privilege across all resources
- *Security Groups & NACLs* – Network access control at multiple layers
- *Audit & Monitoring (planned)* – CloudWatch, AWS Config, or GuardDuty for visibility

## Scalability & Reliability

- *Auto Scaling Groups* – Dynamically scale EC2 instances based on demand
- *Multi-AZ Deployment* – High availability via redundancy across two zones
- *Health Checks via ALB* – Auto-healing and traffic routing to healthy instances



## Infrastructure Notes

- Designed with infrastructure-as-code in mind
- Logical network segregation across public/private layers
- Modular approach to enable future services (e.g., S3, Lambda, RDS)

##  Files Included

- README.md  
- hybrid-architecture images 
- terraform code

##  Next Steps

- Implement Auto Scaling and Monitoring in Terraform
- Expand security policies (e.g., IAM boundary policies)
- Add backup and disaster recovery options (e.g., S3 snapshots, Oracle replication)
- Consider Direct Connect as an upgrade to VPN for long-term throughput

## Author

Khomotso Mashupye   
Cloud Architect-in-Training 

