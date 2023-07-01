# Azure Honeynet & SOC Project: Cyber Attacks in Real Time
![Cloud Honeynet / SOC](https://i.imgur.com/7s0rHfn.png)

## Introduction

 In this project, I simulate a small-scale honeynet that attracts real-world traffic from attackers around the world through Microsoft Azure. The goal throughout this project is to demonstrate best security practices, incident response tactics, and the effects of hardening your environment. We'll accomplish this by intentionally deploying virtual machines that have no safeguard from the public internet to attract attackers into our environment. Then after ingesting some log sources into Log Analytics Workspace, Microsoft Sentinel will come in to create attack maps, alerts, and incidents. In order to showcase metrics before and after hardening the environment based off the incidents generated from the 24 hour capture. 

## Azure Components Utilized

- Azure Virtual Network (VNet)
- Azure Network Security Group (NSG)
- Virtual Machines (2x Windows, 1x Linux)
- Log Analytics Workspace with Kusto Query Language (KQL) Queries
- Azure Key Vault 
- Azure Storage Account 
- Microsoft Sentinel 
- Microsoft Defender for Cloud 


## Architecture Before Hardening
![Architecture Diagram](https://i.imgur.com/c2E0AtK.png)

 - In the "BEFORE" stage of the project, all resources were initially deployed with the hope that attraction would be gained from the public internet. The Virtual Machines had both their Network Security Groups (NSGs) and built-in firewalls wide open, allowing unrestricted access from any source. Additionally, all other resources, such as storage accounts and databases, were deployed with public endpoints visible to the internet, without utilizing any Private Endpoints for added security. These machines were then left to the public for 24 hours to generate the following attack maps mentioned earler. 
 <br />
 
 <b>This attack map showcases the number of incidents generated by leaving the Network Security Group (NSG) open. </b>
 
   ![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/bNOtiKt.png)<br>

 <br />
 <br />
 
 <b>This attack map highlights the incidents for syslog authentication failures experienced by the Linux server. </b>
 
![Linux Syslog Auth Failures](https://i.imgur.com/nFR0Ehf.png)<br>

 <br />
 <br />
 
 <b>This attack map showcases RDP and SMB failures against the Window machine.</b>
 
![Windows RDP/SMB Auth Failures](https://i.imgur.com/4bylhdW.png)<br>

 <br />
 <br />
 
 <b>This attack map showcases failures against the MSSQL server.</b>
 
![MSSQL](https://i.imgur.com/TYIlNVI.png)<br>

 <br />
 <br />
 
 ## After Hardening Measures and Security Controls

In the "AFTER" stage, based off the incidents created from the "Before" 24 hour capture, I implemented hardening measures and security controls to improve the environment's security from attackers.<br /> 
These improvements included:

- <b>Network Security Groups (NSGs)</b>: I hardened the NSGs by only allowing my own public IP address to come thrugh otherwise all other traffic would be blocked by the new parameteres created.

- <b>Built-in Firewalls</b>: In my virtual machines I configured the built-in firewalls so that it would deny access from unauthorized users. 

- <b>Private Endpoints</b>: For other Azure resources, I replaced the public endpoints with Private Endpoints. This ensured that access to sensitive resources, such as storage accounts and databases, was limited to only the virtual network.

