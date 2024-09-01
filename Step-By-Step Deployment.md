# <p align="center"> Building A SOC + Honeynet in Azure (Live Traffic) </br> Step-By-Step Deployment

## Introduction

This project aims to set up a comprehensive Cloud Honeynet integrated with a Security Operations Center (SOC) using Microsoft Azure services. The objective is to deploy a virtualized environment that simulates a vulnerable cloud infrastructure, which is then monitored for security incidents using Microsoft Sentinel. The project provides hands-on experience with setting up cloud resources, configuring security monitoring tools, and analyzing security logs to detect and respond to potential threats.

This project is divided into several parts, starting with the creation of cloud resources in Azure, configuring logging and monitoring using Microsoft Sentinel, and ending with securing the cloud environment based on best practices and compliance standards.

## Table of Contents

- Introduction
- [Part 1: Azure Setup](#Part-1-Azure-Setup)
  - Step 1: Creating Subscription and Resource  
  - Step 2: Installing Microsoft SQL Server
  - Step 3: Security Operations
  - Step 4: Microsoft Entra ID (Azure Active Directory)
- Part 2: Logging and Monitoring
  - Step 1: Geo IP Data Ingestion and Microsoft Sentinel Setup
  - Step 2: Enabling Microsoft Defender for Cloud
  - Step 3: Log Collection for VMs and Network Security Groups
  - Step 4: Logging for Microsoft Entra ID and Other Resources
- Part 3: Microsoft Sentinel (SIEM)
  - Step 1: World Maps Construction
  - Step 2: Automatic Alert Creation
  - Step 3: Running the Insecure Environment
- Part 4: Secure Cloud Configuration
  - Step 1: Containment and Recovery
  - Step 2: Regulatory Compliance
  - Step 3: Securing Resources
  - Step 4: Running the Secure Environment
- Part 5: Environment Cleanup
  - Step 1: Delete Resource Groups
  - Step 2: Remove Microsoft Entra ID Accounts
  - Step 3: Deprovision Subscription and Log Analytics Workspace
- Conclusion    

## <p align="center"> Step-By-Step Deployment

## Part 1: Azure Setup

### Step 1: Creating Subscription and Resource
  - Create our Account (Tenant) and Subscription
    - Create Azure Account (do not user your work or school account)
    - Create Azure Subscription
  - Create Windows 10 Pro Virtual Machine (Name it windows-vm)
    - See all sizes, strong password
    - Region: EAST US 2
    - Name the Resource Group: RG-Cyber-Lab
    - Name the Virtual Network: Lab-VNet
  - Create one more Virtual Machine running Ubuntu (Linux) name it: linux-vm
    - Same Region, Resource Group, and VNet as windows-vm
    - Region: EAST US 2
    - For the VM size, do not choose B1s, choose something larger or it will get DDOS and stop creating logs
    - Ensure you use a username and password instead for authentication
  - Open Network Security Groups for both VMs
    - Configure Network Security Group (Layer 4 Firewall) to allow all traffic inbound
### Step 2: Installing Microsoft SQL Server
  - Disable Windows Firewall and Install SQL Server and Create Vulnerabilities
    - Remote into to the VM (windows-vm)
    - Turn off Windows Firewall
    - Install SQL Server Evaluation
    - Install SSMS (SQL Server Management Studio)
    - Enable logging for SQL Server to be ported to Windows Event Viewer
    - Test SQL logging to make sure it’s working properly
- Test ping and logging into linux-vm via SSH
  - Ping linux-vm
  - Login to linux-vm
### Step 3: Security Operations
- Admin Mode
  - RDP back into windows-vm
  - Inspect the failures and successes (Security Log for RDP, Application log for SQL)
  - Take notes of the EventIDs, messaging, Source IP addresses, etc
- SSH into the linux-vm, observe logs with the following commands
    
      cat /var/logs/auth.log | grep password 
      cat /var/logs/auth.log | grep Accepted

### Step 4: Microsoft Entra ID (Azure Active Directory)


## Conclusion

This project provides a comprehensive guide to setting up a secure cloud environment, simulating real-world attacks, and monitoring security events using Azure and Microsoft Sentinel. By following the steps outlined, you will gain practical experience in cloud security operations, including the deployment of a honeynet, configuration of security monitoring tools, and implementation of security controls to protect cloud resources. The project emphasizes the importance of continuous monitoring and compliance in maintaining a secure cloud infrastructure.

