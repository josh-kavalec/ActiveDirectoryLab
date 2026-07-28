# Active Directory Lab
This project documents the creation of a fully functional Active Directory home lab using Oracle VirtualBox. The environment consists of a Windows Server 2022 domain controller and a Windows 11 client connected through an isolated virtual network. The lab demonstrates the deployment and configuration of Active Directory Domain Services (AD DS), DNS, DHCP, RAS/NAT, and PowerShell automation to simulate a small enterprise environment. 

# Environments and Utilities Used
- Oracle VirtualBox
- Windows Server 2022
- Windows 11
- PowerShell

# Project Overview: Network Diagram

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Full%20Diagram.png?raw=true)

<h1 align="center">Step 1:</h1>
The first virtual machine created is the Domain Controller which is where Active Directory is created. This virtual machine contains two network adapters, one that connects to the Internet on the outside, and another that connects to the Internal network on the inside that clients will connect to. After the virtual machine is created, Windows Server 2022 is installed and will be assigned an IP address to the Internal network. The external network will automatically be assigned an IP address from the home router (DHCP). 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%201.png?raw=true)

<h1 align="center">Step 2:</h1>
After we assign the IP address, we will name the server and will install an active directory and create our domain. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%202.png?raw=true)

<h1 align="center">Step 3:</h1>
We are then going to configure NAT and Routing so that clients on the internal network will be able to access the internet through the Domain Controller. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%203.png?raw=true)

<h1 align="center">Step 4:</h1>
Next we’re going to set up DHCP on the Domain Controller so when we create a Windows 11 machine it will automatically be assigned an IP Address. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%204.png?raw=true)

<h1 align="center">Step 5:</h1>
Before we create our client virtual machine, the final thing we do in the Domain Controller is we’re going to run a PowerShell script that will automatically create a thousand users in Active Directory. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshopt%205.png?raw=true)

<h1 align="center">Step 6:</h1>
After creating the users, we’re going to create another virtual machine and install Windows 11 and that virtual machine will be connected to the private VirtualBox network. We will name that machine Client 1 and join it to the domain. We will then log in with one of the domain accounts.

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%206.png?raw=true)

# Step-by-Step Project Walkthrough

We created our first virtual machine labeled “Domain Controller” in which I currently have Windows Server 2022 Installed. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%207.png?raw=true)

We will then proceed to configure the virtual machine labeled “Domain Controller.” Clicking on Settings, and clicking onto the Network tab, we can see that we currently have one Network Adapter connected. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%208.png?raw=true)

Based on the Network Diagram previously listed, we have two network adapters connected to the Domain Controller. We must select Adapter Two and Enable Network Adapter. Next to the “Attached to” dropdown, we will select Internal Network. This is because we already have one dedicated for the Internet, and now we have one for our Internal Network. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%209.png?raw=true)

