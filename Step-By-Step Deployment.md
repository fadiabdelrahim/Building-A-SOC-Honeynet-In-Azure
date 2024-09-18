# <p align="center"> Building A SOC + Honeynet in Azure (Live Traffic) </br> Step-By-Step Deployment

## Introduction

This project aims to set up a comprehensive Cloud Honeynet integrated with a Security Operations Center (SOC) using Microsoft Azure services. The objective is to deploy a virtualized environment that simulates a vulnerable cloud infrastructure, which is then monitored for security incidents using Microsoft Sentinel. The project provides hands-on experience with setting up cloud resources, configuring security monitoring tools, and analyzing security logs to detect and respond to potential threats.

This project is divided into several parts, starting with the creation of cloud resources in Azure, configuring logging and monitoring using Microsoft Sentinel, and ending with securing the cloud environment based on best practices and compliance standards.

## Table of Contents

- [Introduction](#Introduction)
- [Part 1: Azure Setup](#Part-1-Azure-Setup)
  - [Step 1: Creating Subscription and Resource](#Step-1-Creating-Subscription-and-Resource)  
  - [Step 2: Installing Microsoft SQL Server](#Step-2-Installing-Microsoft-SQL-Server)
  - [Step 3: Security Operations](#Step-3-Security-Operations)
  - [Step 4: Microsoft Entra ID (Azure Active Directory)](#Step-4-Microsoft-Entra-ID-Azure-Active-Directory)
- [Part 2: Logging and Monitoring](#Part-2-Logging-and-Monitoring)
  - [Step 1: Geo IP Data Ingestion and Microsoft Sentinel Setup](#Step-1-Geo-IP-Data-Ingestion-and-Microsoft-Sentinel-Setup)
  - [Step 2: Enabling Microsoft Defender for Cloud](#Step-2-Enabling-Microsoft-Defender-for-Cloud)
  - [Step 3: Log Collection for VMs and Network Security Groups](#Step-3-Log-Collection-for-VMs-and-Network-Security-Groups)
  - [Step 4: Logging for Microsoft Entra ID and Other Resources](#Step-4-Logging-for-Microsoft-Entra-ID-and-Other-Resources)
  - [Step 5: Subscription Level Logging (Activity Log)](#Step-5-Subscription-Level-Logging-Activity-Log)
  - [Step 6: Resource Level Logging](#Step-6-Resource-Level-Logging)
- [Part 3: Microsoft Sentinel (SIEM)](#Part-3-Microsoft-Sentinel-SIEM)
  - [Step 1: World Maps Construction](#Step-1-World-Maps-Construction)
  - [Step 2: Automatic Alert Creation](#Step-2-Automatic-Alert-Creation)
  - [Step 3: Running the Insecure Environment](#Step-3-Running-the-Insecure-Environment)
- [Part 4: Secure Cloud Configuration](#Part-4-Secure-Cloud-Configuration)
  - [Step 1: Containment and Recovery](#Step-1-Containment-and-Recovery)
  - [Step 2: Regulatory Compliance](#Step-2-Regulatory-Compliance)
  - [Step 3: Securing Resources](#Step-3-Securing-Resources)
  - [Step 4: Running the Secure Environment](#Step-4-Running-the-Secure-Environment)
- [Part 5: Environment Cleanup](#Part-5-Environment-Cleanup)
  - [Step 1: Delete Resource Groups](#Step-1-Delete-Resource-Groups)
  - [Step 2: Remove Microsoft Entra ID Accounts](#Step-2-Remove-Microsoft-Entra-ID-Accounts)
  - [Step 3: Deprovision Subscription and Log Analytics Workspace](#Step-3-Deprovision-Subscription-and-Log-Analytics-Workspace)
- [Conclusion](#Conclusion)    

## <p align="center"> Step-By-Step Deployment

## Part 1: Azure Setup

### <ins>Step 1: Creating Subscription and Resource</ins>
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
   
<p align="center"><img src="images/Picture1.png"></p>
<p align="center"><img src="images/Picture2.png"></p>
<p align="center"><img src="images/Picture3.png"></p>
<p align="center"><img src="images/Picture4.png"></p>
<p align="center"><img src="images/Picture5.png"></p>
<p align="center"><img src="images/Picture6.png"></p>
<p align="center"><img src="images/Picture7.png"></p>
<p align="center"><img src="images/Picture8.png"></p>
<p align="center"><img src="images/Picture9.png"></p>
<p align="center"><img src="images/Picture10.png"></p>
<p align="center"><img src="images/Picture11.png"></p>
<p align="center"><img src="images/Picture12.png"></p>
<p align="center"><img src="images/Picture13.png"></p>
<p align="center"><img src="images/Picture14.png"></p>
<p align="center"><img src="images/Picture15.png"></p>
<p align="center"><img src="images/Picture16.png"></p>
<p align="center"><img src="images/Picture17.png"></p>
<p align="center"><img src="images/Picture18.png"></p>
<p align="center"><img src="images/Picture19.png"></p>
<p align="center"><img src="images/Picture20.png"></p>
<p align="center"><img src="images/Picture21.png"></p>
<p align="center"><img src="images/Picture22.png"></p>
<p align="center"><img src="images/Picture23.png"></p>
<p align="center"><img src="images/Picture24.png"></p>
<p align="center"><img src="images/Picture25.png"></p>
<p align="center"><img src="images/Picture26.png"></p>
<p align="center"><img src="images/Picture27.png"></p>
<p align="center"><img src="images/Picture28.png"></p>
<p align="center"><img src="images/Picture29.png"></p>
<p align="center"><img src="images/Picture30.png"></p>
<p align="center"><img src="images/Picture31.png"></p>
<p align="center"><img src="images/Picture32.png"></p>
<p align="center"><img src="images/Picture33.png"></p>
<p align="center"><img src="images/Picture34.png"></p>
<p align="center"><img src="images/Picture35.png"></p>
<p align="center"><img src="images/Picture36.png"></p>
<p align="center"><img src="images/Picture37.png"></p>
<p align="center"><img src="images/Picture38.png"></p>
<p align="center"><img src="images/Picture39.png"></p>
<p align="center"><img src="images/Picture40.png"></p>
<p align="center"><img src="images/Picture41.png"></p>
<p align="center"><img src="images/Picture42.png"></p>
<p align="center"><img src="images/Picture43.png"></p>
<p align="center"><img src="images/Picture44.png"></p>
<p align="center"><img src="images/Picture45.png"></p>
<p align="center"><img src="images/Picture46.png"></p>
<p align="center"><img src="images/Picture47.png"></p>
<p align="center"><img src="images/Picture48.png"></p>
<p align="center"><img src="images/Picture49.png"></p>
<p align="center"><img src="images/Picture50.png"></p>
<p align="center"><img src="images/Picture51.png"></p>
<p align="center"><img src="images/Picture52.png"></p>
<p align="center"><img src="images/Picture53.png"></p>
<p align="center"><img src="images/Picture54.png"></p>
<p align="center"><img src="images/Picture55.png"></p>
<p align="center"><img src="images/Picture56.png"></p>

### <ins>Step 2: Installing Microsoft SQL Server</ins>
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

<p align="center"><img src="images/Picture57.png"></p>
<p align="center"><img src="images/Picture58.png"></p>
<p align="center"><img src="images/Picture59.png"></p>
<p align="center"><img src="images/Picture60.png"></p>
<p align="center"><img src="images/Picture61.png"></p>
<p align="center"><img src="images/Picture62.png"></p>
<p align="center"><img src="images/Picture63.png"></p>
<p align="center"><img src="images/Picture64.png"></p>
<p align="center"><img src="images/Picture65.png"></p>
<p align="center"><img src="images/Picture66.png"></p>
<p align="center"><img src="images/Picture67.png"></p>
<p align="center"><img src="images/Picture68.png"></p>
<p align="center"><img src="images/Picture69.png"></p>
<p align="center"><img src="images/Picture70.png"></p>
<p align="center"><img src="images/Picture71.png"></p>
<p align="center"><img src="images/Picture72.png"></p>
<p align="center"><img src="images/Picture73.png"></p>
<p align="center"><img src="images/Picture74.png"></p>
<p align="center"><img src="images/Picture75.png"></p>
<p align="center"><img src="images/Picture76.png"></p>
<p align="center"><img src="images/Picture77.png"></p>
<p align="center"><img src="images/Picture78.png"></p>
<p align="center"><img src="images/Picture79.png"></p>
<p align="center"><img src="images/Picture80.png"></p>
<p align="center"><img src="images/Picture81.png"></p>
<p align="center"><img src="images/Picture82.png"></p>
<p align="center"><img src="images/Picture83.png"></p>
<p align="center"><img src="images/Picture84.png"></p>
<p align="center"><img src="images/Picture85.png"></p>
<p align="center"><img src="images/Picture86.png"></p>
<p align="center"><img src="images/Picture87.png"></p>
<p align="center"><img src="images/Picture88.png"></p>
<p align="center"><img src="images/Picture89.png"></p>
<p align="center"><img src="images/Picture90.png"></p>
<p align="center"><img src="images/Picture91.png"></p>
<p align="center"><img src="images/Picture92.png"></p>
<p align="center"><img src="images/Picture93.png"></p>
<p align="center"><img src="images/Picture94.png"></p>
<p align="center"><img src="images/Picture95.png"></p>
<p align="center"><img src="images/Picture96.png"></p>
<p align="center"><img src="images/Picture97.png"></p>
<p align="center"><img src="images/Picture98.png"></p>
<p align="center"><img src="images/Picture99.png"></p>
<p align="center"><img src="images/Picture100.png"></p>
<p align="center"><img src="images/Picture101.png"></p>
<p align="center"><img src="images/Picture102.png"></p>
<p align="center"><img src="images/Picture103.png"></p>
<p align="center"><img src="images/Picture104.png"></p>
<p align="center"><img src="images/Picture105.png"></p>
<p align="center"><img src="images/Picture106.png"></p>
<p align="center"><img src="images/Picture107.png"></p>
<p align="center"><img src="images/Picture108.png"></p>
<p align="center"><img src="images/Picture109.png"></p>
<p align="center"><img src="images/Picture110.png"></p>
<p align="center"><img src="images/Picture111.png"></p>
<p align="center"><img src="images/Picture112.png"></p>
<p align="center"><img src="images/Picture113.png"></p>
<p align="center"><img src="images/Picture114.png"></p>
<p align="center"><img src="images/Picture115.png"></p>
<p align="center"><img src="images/Picture116.png"></p>
<p align="center"><img src="images/Picture117.png"></p>
<p align="center"><img src="images/Picture118.png"></p>

### <ins>Step 3: Security Operations</ins>
- Admin Mode
  - RDP back into windows-vm
  - Inspect the failures and successes (Security Log for RDP, Application log for SQL)
  - Take notes of the EventIDs, messaging, Source IP addresses, etc
- SSH into the linux-vm, observe logs with the following commands
    
      cat /var/logs/auth.log | grep password 
      cat /var/logs/auth.log | grep Accepted

<p align="center"><img src="images/Picture119.png"></p>
<p align="center"><img src="images/Picture120.png"></p>
<p align="center"><img src="images/Picture121.png"></p>
<p align="center"><img src="images/Picture122.png"></p>
<p align="center"><img src="images/Picture123.png"></p>
<p align="center"><img src="images/Picture124.png"></p>
<p align="center"><img src="images/Picture125.png"></p>
<p align="center"><img src="images/Picture126.png"></p>
<p align="center"><img src="images/Picture127.png"></p>
<p align="center"><img src="images/Picture128.png"></p>
<p align="center"><img src="images/Picture129.png"></p>
<p align="center"><img src="images/Picture130.png"></p>
<p align="center"><img src="images/Picture131.png"></p>
<p align="center"><img src="images/Picture132.png"></p>

### <ins>Step 4: Microsoft Entra ID (Azure Active Directory)</ins>
- Configure Tenant-Level Global Reader
  - Create a user within Microsoft Entra ID (username: globalreaderjohn)
    - Assing Tenant-Level Global Reader
- Configure Subscription Reader
  - Create another user with Microsoft Entra ID (username: subreaderjane)
    - Assign Subscription-Level Reader
- Configure Resource Group Contributor (like an admin)
  - Create another user within Microsoft Entra ID (username: rgcontributordave)
    - Assign Resource Group-level Contributor
    - For resource group (RG-Cyber-Lab), assign Contributor Permissions

<p align="center"><img src="images/Picture133.png"></p>
<p align="center"><img src="images/Picture134.png"></p>
<p align="center"><img src="images/Picture135.png"></p>
<p align="center"><img src="images/Picture136.png"></p>
<p align="center"><img src="images/Picture137.png"></p>
<p align="center"><img src="images/Picture138.png"></p>
<p align="center"><img src="images/Picture139.png"></p>
<p align="center"><img src="images/Picture140.png"></p>
<p align="center"><img src="images/Picture141.png"></p>
<p align="center"><img src="images/Picture142.png"></p>
<p align="center"><img src="images/Picture143.png"></p>
<p align="center"><img src="images/Picture144.png"></p>
<p align="center"><img src="images/Picture145.png"></p>
<p align="center"><img src="images/Picture146.png"></p>
<p align="center"><img src="images/Picture147.png"></p>
<p align="center"><img src="images/Picture148.png"></p>
<p align="center"><img src="images/Picture149.png"></p>
<p align="center"><img src="images/Picture150.png"></p>
<p align="center"><img src="images/Picture151.png"></p>
<p align="center"><img src="images/Picture152.png"></p>
<p align="center"><img src="images/Picture153.png"></p>
<p align="center"><img src="images/Picture154.png"></p>
<p align="center"><img src="images/Picture155.png"></p>
<p align="center"><img src="images/Picture156.png"></p>
<p align="center"><img src="images/Picture157.png"></p>
<p align="center"><img src="images/Picture158.png"></p>
<p align="center"><img src="images/Picture159.png"></p>
<p align="center"><img src="images/Picture160.png"></p>
<p align="center"><img src="images/Picture161.png"></p>
<p align="center"><img src="images/Picture162.png"></p>
<p align="center"><img src="images/Picture163.png"></p>
<p align="center"><img src="images/Picture164.png"></p>
<p align="center"><img src="images/Picture165.png"></p>
<p align="center"><img src="images/Picture166.png"></p>
   
## Part 2: Logging and Monitoring

### <ins>Step 1: Geo IP Data Ingestion and Microsoft Sentinel Setup</ins>
- Add Large Geo-Data Files in Azure Storage
  - Use geoip-summarized.csv file
- Create a Log Analytics Workspace (log aggregator) named: LAW-Cyber-Lab
- Setup Sentinel and connect it to Log Analytics Workspace
  - Create the geoip watchlist
    - Name/Alias: geoip
    - Source type: Local File
    - Number of lines before row: 0
    - Search Key: network
  - Use _GetWatchlist(“geoip”) in Log Analytics Workspace to verify Geo-Data has loaded

<p align="center"><img src="images/Picture167.png"></p>
<p align="center"><img src="images/Picture168.png"></p>
<p align="center"><img src="images/Picture169.png"></p>
<p align="center"><img src="images/Picture170.png"></p>
<p align="center"><img src="images/Picture171.png"></p>
<p align="center"><img src="images/Picture172.png"></p>
<p align="center"><img src="images/Picture173.png"></p>
<p align="center"><img src="images/Picture174.png"></p>
<p align="center"><img src="images/Picture175.png"></p>
<p align="center"><img src="images/Picture176.png"></p>
<p align="center"><img src="images/Picture177.png"></p>
<p align="center"><img src="images/Picture178.png"></p>
<p align="center"><img src="images/Picture179.png"></p>
<p align="center"><img src="images/Picture180.png"></p>
<p align="center"><img src="images/Picture181.png"></p>
<p align="center"><img src="images/Picture182.png"></p>
<p align="center"><img src="images/Picture183.png"></p>
<p align="center"><img src="images/Picture184.png"></p>
<p align="center"><img src="images/Picture185.png"></p>
<p align="center"><img src="images/Picture186.png"></p>
<p align="center"><img src="images/Picture187.png"></p>
<p align="center"><img src="images/Picture188.png"></p>

### <ins>Step 2: Enabling Microsoft Defender for Cloud</ins>
- Enable Microsoft Defender for Cloud for Log Analytics Workspace
  - Enable Defender Plans for VMs and SQL Instances on VMs
  - Enable Data Collection (All Events)
- Enable Microsoft Defender for Cloud for Subscription
  - VMs, Storage Accounts, Key Vault, SQL Server
  - Make sure logs are being sent to correct log analytics workspaces
- Enable Microsoft Defender for Cloud Continuous Export in Environment Settings
  - Export to the correct Log Analytics Workspace

<p align="center"><img src="images/Picture189.png"></p>
<p align="center"><img src="images/Picture190.png"></p>
<p align="center"><img src="images/Picture191.png"></p>
<p align="center"><img src="images/Picture192.png"></p>
<p align="center"><img src="images/Picture193.png"></p>
<p align="center"><img src="images/Picture194.png"></p>
<p align="center"><img src="images/Picture195.png"></p>
<p align="center"><img src="images/Picture196.png"></p>
<p align="center"><img src="images/Picture197.png"></p>
<p align="center"><img src="images/Picture198.png"></p>
<p align="center"><img src="images/Picture199.png"></p>
<p align="center"><img src="images/Picture200.png"></p>
<p align="center"><img src="images/Picture201.png"></p>
<p align="center"><img src="images/Picture202.png"></p>

### <ins>Step 3: Log Collection for VMs and Network Security Groups</ins>
- Create Azure Storage Account (sacyberlab01)
  - Must be in the same region as VMs
  - This will be used to store the NSG Flow Logs
- Enable Flow logs for both Network Security Groups (NSGs)
- Configure Data Collection Rules within our Log Analytics Workspace
  - Configure Linux Data Sources (auth only)
    - Linux-vm-logs
  - Configure Windows Data Sources (Application-information only, Security-All)
    - Windows-vm-logs
  - Configure Special Windows Event Data Collection (Defender and Windows Firewall)
- Manually install the Log Analytics Agent on both windows-vm and linux-vm
- Query Log Analytics for logs from the VMs and NSGs
  - Syslog (linux)
  - SecurityEvent (windows)
  - AzureNetworkAnalytics_CL (NSGs)

<p align="center"><img src="images/Picture203.png"></p>
<p align="center"><img src="images/Picture204.png"></p>
<p align="center"><img src="images/Picture205.png"></p>
<p align="center"><img src="images/Picture206.png"></p>
<p align="center"><img src="images/Picture207.png"></p>
<p align="center"><img src="images/Picture208.png"></p>
<p align="center"><img src="images/Picture209.png"></p>
<p align="center"><img src="images/Picture210.png"></p>
<p align="center"><img src="images/Picture211.png"></p>
<p align="center"><img src="images/Picture212.png"></p>
<p align="center"><img src="images/Picture213.png"></p>
<p align="center"><img src="images/Picture214.png"></p>
<p align="center"><img src="images/Picture215.png"></p>
<p align="center"><img src="images/Picture216.png"></p>
<p align="center"><img src="images/Picture217.png"></p>
<p align="center"><img src="images/Picture218.png"></p>
<p align="center"><img src="images/Picture219.png"></p>
<p align="center"><img src="images/Picture220.png"></p>
<p align="center"><img src="images/Picture221.png"></p>
<p align="center"><img src="images/Picture222.png"></p>
<p align="center"><img src="images/Picture223.png"></p>
<p align="center"><img src="images/Picture224.png"></p>
<p align="center"><img src="images/Picture225.png"></p>
<p align="center"><img src="images/Picture226.png"></p>
<p align="center"><img src="images/Picture227.png"></p>
<p align="center"><img src="images/Picture228.png"></p>
<p align="center"><img src="images/Picture229.png"></p>
<p align="center"><img src="images/Picture230.png"></p>
<p align="center"><img src="images/Picture231.png"></p>
<p align="center"><img src="images/Picture232.png"></p>
<p align="center"><img src="images/Picture233.png"></p>
<p align="center"><img src="images/Picture234.png"></p>
<p align="center"><img src="images/Picture235.png"></p>
<p align="center"><img src="images/Picture236.png"></p>
<p align="center"><img src="images/Picture237.png"></p>
<p align="center"><img src="images/Picture238.png"></p>
<p align="center"><img src="images/Picture239.png"></p>
<p align="center"><img src="images/Picture240.png"></p>
<p align="center"><img src="images/Picture241.png"></p>
<p align="center"><img src="images/Picture242.png"></p>
<p align="center"><img src="images/Picture243.png"></p>
<p align="center"><img src="images/Picture244.png"></p>
<p align="center"><img src="images/Picture245.png"></p>

### <ins>Step 4: Logging for Microsoft Entra ID and Other Resources</ins>
- Create Diagnostic Settings to ingest Microsoft Entra ID logs
  - Enable Audit logs and Sign in Logs for Microsoft Entra ID

<p align="center"><img src="images/Picture246.png"></p>
<p align="center"><img src="images/Picture247.png"></p>
<p align="center"><img src="images/Picture248.png"></p>
<p align="center"><img src="images/Picture249.png"></p>

### <ins>Step 5: Subscription Level Logging (Activity Log)</ins>
- Export Azure Activity Logs to Log Analytics Workspace

<p align="center"><img src="images/Picture250.png"></p>
<p align="center"><img src="images/Picture251.png"></p>
<p align="center"><img src="images/Picture252.png"></p>
<p align="center"><img src="images/Picture253.png"></p>

### <ins>Step 6: Resource Level Logging</ins>
- Configure Logging for Azure Storage
  - Configure logging for storage account by enabling diagnostics settings for blob storage
-  Configure Logging for Key Vault
  -  Create a Key Vault Instance and collect the audit log and send to Log Analytics Workspace

<p align="center"><img src="images/Picture254.png"></p>
<p align="center"><img src="images/Picture255.png"></p>
<p align="center"><img src="images/Picture256.png"></p>
<p align="center"><img src="images/Picture257.png"></p>
<p align="center"><img src="images/Picture258.png"></p>
<p align="center"><img src="images/Picture259.png"></p>
<p align="center"><img src="images/Picture260.png"></p>
<p align="center"><img src="images/Picture261.png"></p>
<p align="center"><img src="images/Picture262.png"></p>
<p align="center"><img src="images/Picture263.png"></p>
<p align="center"><img src="images/Picture264.png"></p>
<p align="center"><img src="images/Picture265.png"></p>
<p align="center"><img src="images/Picture266.png"></p>
<p align="center"><img src="images/Picture267.png"></p>
<p align="center"><img src="images/Picture268.png"></p>
<p align="center"><img src="images/Picture269.png"></p>
<p align="center"><img src="images/Picture270.png"></p>

## Part 3: Microsoft Sentinel (SIEM)

### <ins>Step 1: World Maps Construction</ins>
- Within Azure Sentinel create the following workbooks
  - windows-rdp-auth-fail.json – Create the Windows RDP/SMB Authentication Failure map
  - linux-ssh-auth-fail.json – Create the Linux SSH Authentication Failures map
  - mssql-auth-fail.json – Create MS SQL Server Authentication Failures map
  - nsg-malicious-allowed-in.json – Create the NSG Allowed Malicious Inbound

<p align="center"><img src="images/Picture271.png"></p>
<p align="center"><img src="images/Picture272.png"></p>
<p align="center"><img src="images/Picture273.png"></p>
<p align="center"><img src="images/Picture274.png"></p>
<p align="center"><img src="images/Picture275.png"></p>
<p align="center"><img src="images/Picture276.png"></p>
<p align="center"><img src="images/Picture277.png"></p>
<p align="center"><img src="images/Picture278.png"></p>
<p align="center"><img src="images/Picture279.png"></p>
<p align="center"><img src="images/Picture280.png"></p>
<p align="center"><img src="images/Picture281.png"></p>
<p align="center"><img src="images/Picture282.png"></p>
<p align="center"><img src="images/Picture283.png"></p>
<p align="center"><img src="images/Picture284.png"></p>
<p align="center"><img src="images/Picture285.png"></p>
<p align="center"><img src="images/Picture286.png"></p>
<p align="center"><img src="images/Picture287.png"></p>
<p align="center"><img src="images/Picture288.png"></p>
<p align="center"><img src="images/Picture289.png"></p>
<p align="center"><img src="images/Picture290.png"></p>
<p align="center"><img src="images/Picture291.png"></p>
<p align="center"><img src="images/Picture292.png"></p>
<p align="center"><img src="images/Picture293.png"></p>
<p align="center"><img src="images/Picture294.png"></p>
<p align="center"><img src="images/Picture295.png"></p>
<p align="center"><img src="images/Picture296.png"></p>
<p align="center"><img src="images/Picture297.png"></p>
<p align="center"><img src="images/Picture298.png"></p>
<p align="center"><img src="images/Picture299.png"></p>
<p align="center"><img src="images/Picture300.png"></p>
<p align="center"><img src="images/Picture301.png"></p>
<p align="center"><img src="images/Picture302.png"></p>
<p align="center"><img src="images/Picture303.png"></p>
<p align="center"><img src="images/Picture304.png"></p>
<p align="center"><img src="images/Picture305.png"></p>
<p align="center"><img src="images/Picture306.png"></p>
<p align="center"><img src="images/Picture307.png"></p>
<p align="center"><img src="images/Picture308.png"></p>
<p align="center"><img src="images/Picture309.png"></p>
<p align="center"><img src="images/Picture310.png"></p>
<p align="center"><img src="images/Picture311.png"></p>

### <ins>Step 2: Automatic Alert Creation</ins>
- Import all Sentinel Analytics Rules

<p align="center"><img src="images/Picture312.png"></p>
<p align="center"><img src="images/Picture313.png"></p>
<p align="center"><img src="images/Picture314.png"></p>
<p align="center"><img src="images/Picture315.png"></p>
<p align="center"><img src="images/Picture316.png"></p>

### <ins>Step 3: Running the Insecure Environment</ins>
- Let the environment sit for 24 hours
- Count all the alerts that happened in last 24 hours

<p align="center"><img src="images/Picture317.png"></p>
<p align="center"><img src="images/Picture318.png"></p>
<p align="center"><img src="images/Picture319.png"></p>
<p align="center"><img src="images/Picture320.png"></p>
<p align="center"><img src="images/Picture321.png"></p>
<p align="center"><img src="images/Picture322.png"></p>
<p align="center"><img src="images/Picture323.png"></p>
<p align="center"><img src="images/Picture324.png"></p>
<p align="center"><img src="images/Picture325.png"></p>
<p align="center"><img src="images/Picture326.png"></p>
<p align="center"><img src="images/Picture327.png"></p>
<p align="center"><img src="images/Picture328.png"></p>
<p align="center"><img src="images/Picture329.png"></p>
<p align="center"><img src="images/Picture330.png"></p>
<p align="center"><img src="images/Picture331.png"></p>
<p align="center"><img src="images/Picture332.png"></p>
<p align="center"><img src="images/Picture333.png"></p>
<p align="center"><img src="images/Picture334.png"></p>
<p align="center"><img src="images/Picture335.png"></p>
<p align="center"><img src="images/Picture336.png"></p>
<p align="center"><img src="images/Picture337.png"></p>
<p align="center"><img src="images/Picture338.png"></p>
<p align="center"><img src="images/Picture339.png"></p>
<p align="center"><img src="images/Picture340.png"></p>
<p align="center"><img src="images/Picture341.png"></p>
<p align="center"><img src="images/Picture342.png"></p>
<p align="center"><img src="images/Picture343.png"></p>
<p align="center"><img src="images/Picture344.png"></p>
<p align="center"><img src="images/Picture345.png"></p>
<p align="center"><img src="images/Picture346.png"></p>
<p align="center"><img src="images/Picture347.png"></p>
<p align="center"><img src="images/Picture348.png"></p>
<p align="center"><img src="images/Picture349.png"></p>
<p align="center"><img src="images/Picture350.png"></p>

## Part 4: Secure Cloud Configuration

### <ins>Step1: Containment and Recovery</ins>
- Lock down the NSG assigned to the VMs to allow only necessary traffic

<p align="center"><img src="images/Picture351.png"></p>
<p align="center"><img src="images/Picture352.png"></p>
<p align="center"><img src="images/Picture353.png"></p>
<p align="center"><img src="images/Picture354.png"></p>
<p align="center"><img src="images/Picture355.png"></p>
<p align="center"><img src="images/Picture356.png"></p>
<p align="center"><img src="images/Picture357.png"></p>
<p align="center"><img src="images/Picture358.png"></p>
<p align="center"><img src="images/Picture359.png"></p>
<p align="center"><img src="images/Picture360.png"></p>
<p align="center"><img src="images/Picture361.png"></p>
<p align="center"><img src="images/Picture362.png"></p>

### <ins>Step 2: Regulatory Compliance (Enable NIST 800-53)</ins>
- Enable MDC Regulatory Compliance (NIST 800-53)

<p align="center"><img src="images/Picture363.png"></p>
<p align="center"><img src="images/Picture364.png"></p>
<p align="center"><img src="images/Picture365.png"></p>
<p align="center"><img src="images/Picture366.png"></p>
<p align="center"><img src="images/Picture367.png"></p>
<p align="center"><img src="images/Picture368.png"></p>
<p align="center"><img src="images/Picture369.png"></p>
<p align="center"><img src="images/Picture370.png"></p>

### <ins>Step 3: Securing Resources (NIST SC-7)</ins>
- Implement SC-7
- Configure Azure Private Link and Firewall for Azure Key Vault Instances
- Configure Azure Private Link and Firewall for Azure Storage Account Instance
  - Disable Public Access
- Login to windows-vm and check the IP address of Key Vault and Storage Account Instance
- Create NSG and attach to subnet

<p align="center"><img src="images/Picture371.png"></p>
<p align="center"><img src="images/Picture372.png"></p>
<p align="center"><img src="images/Picture373.png"></p>
<p align="center"><img src="images/Picture374.png"></p>
<p align="center"><img src="images/Picture375.png"></p>
<p align="center"><img src="images/Picture376.png"></p>
<p align="center"><img src="images/Picture377.png"></p>
<p align="center"><img src="images/Picture378.png"></p>
<p align="center"><img src="images/Picture379.png"></p>
<p align="center"><img src="images/Picture380.png"></p>
<p align="center"><img src="images/Picture381.png"></p>
<p align="center"><img src="images/Picture382.png"></p>
<p align="center"><img src="images/Picture383.png"></p>
<p align="center"><img src="images/Picture384.png"></p>
<p align="center"><img src="images/Picture385.png"></p>
<p align="center"><img src="images/Picture386.png"></p>
<p align="center"><img src="images/Picture387.png"></p>
<p align="center"><img src="images/Picture388.png"></p>
<p align="center"><img src="images/Picture389.png"></p>
<p align="center"><img src="images/Picture390.png"></p>
<p align="center"><img src="images/Picture391.png"></p>
<p align="center"><img src="images/Picture392.png"></p>
<p align="center"><img src="images/Picture393.png"></p>
<p align="center"><img src="images/Picture394.png"></p>
<p align="center"><img src="images/Picture395.png"></p>
<p align="center"><img src="images/Picture396.png"></p>
<p align="center"><img src="images/Picture397.png"></p>
<p align="center"><img src="images/Picture398.png"></p>
<p align="center"><img src="images/Picture399.png"></p>
<p align="center"><img src="images/Picture400.png"></p>
<p align="center"><img src="images/Picture401.png"></p>
<p align="center"><img src="images/Picture402.png"></p>
<p align="center"><img src="images/Picture403.png"></p>
<p align="center"><img src="images/Picture404.png"></p>
<p align="center"><img src="images/Picture405.png"></p>
<p align="center"><img src="images/Picture406.png"></p>
<p align="center"><img src="images/Picture407.png"></p>

### <ins>Step 4: Running the Secure Environment</ins> 
- Let the environment sit for 24 hours
- Count all the alerts that happened in last 24 hours

<p align="center"><img src="images/Picture408.png"></p>
<p align="center"><img src="images/Picture409.png"></p>
<p align="center"><img src="images/Picture410.png"></p>
<p align="center"><img src="images/Picture411.png"></p>
<p align="center"><img src="images/Picture412.png"></p>
<p align="center"><img src="images/Picture413.png"></p>
<p align="center"><img src="images/Picture414.png"></p>
<p align="center"><img src="images/Picture415.png"></p>

## Part 5: Environment Cleanup

### <ins>Step 1: Delete Resource Groups</ins>
- Delete all resource groups

<p align="center"><img src="images/Picture416.png"></p>
<p align="center"><img src="images/Picture417.png"></p>
<p align="center"><img src="images/Picture418.png"></p>
<p align="center"><img src="images/Picture419.png"></p>
<p align="center"><img src="images/Picture420.png"></p>
<p align="center"><img src="images/Picture421.png"></p>
<p align="center"><img src="images/Picture422.png"></p>
<p align="center"><img src="images/Picture423.png"></p>
<p align="center"><img src="images/Picture424.png"></p>
<p align="center"><img src="images/Picture425.png"></p>
<p align="center"><img src="images/Picture426.png"></p>

### <ins>Step 2: Remove Microsoft Entra ID Accounts</ins>
- Go to Microsoft Entra ID and delete all accounts
- In Microsoft Entra ID ensure diagnostic settings have been deleted

<p align="center"><img src="images/Picture427.png"></p>
<p align="center"><img src="images/Picture428.png"></p>
<p align="center"><img src="images/Picture429.png"></p>
<p align="center"><img src="images/Picture430.png"></p>
<p align="center"><img src="images/Picture431.png"></p>
<p align="center"><img src="images/Picture432.png"></p>

### <ins>Step 3: Deprovision Subscription and Log Analytics Workspace</ins>
- Go to Microsoft Defender for Cloud -> Environment Settings and deprovision the subscription and Log Analytics Workspace

<p align="center"><img src="images/Picture433.png"></p>
<p align="center"><img src="images/Picture434.png"></p>
<p align="center"><img src="images/Picture435.png"></p>
<p align="center"><img src="images/Picture436.png"></p>
<p align="center"><img src="images/Picture437.png"></p>

## Conclusion

This project provides a comprehensive guide to setting up a secure cloud environment, simulating real-world attacks, and monitoring security events using Azure and Microsoft Sentinel. By following the steps outlined, you will gain practical experience in cloud security operations, including the deployment of a honeynet, configuration of security monitoring tools, and implementation of security controls to protect cloud resources. The project emphasizes the importance of continuous monitoring and compliance in maintaining a secure cloud infrastructure.

