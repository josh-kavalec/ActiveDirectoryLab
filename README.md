# Active Directory Lab
This project documents the creation of a fully functional Active Directory home lab using Oracle VirtualBox. The environment consists of a Windows Server 2022 domain controller and a Windows 11 client connected through an isolated virtual network. The lab demonstrates the deployment and configuration of Active Directory Domain Services (AD DS), DNS, DHCP, RAS/NAT, and PowerShell automation to simulate a small enterprise environment. 

# Environments and Utilities Used
- Oracle VirtualBox
- Windows Server 2022
- Windows 11
- PowerShell

<h1 align="center">Network Diagram</h1>

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Full%20Diagram.png?raw=true)

<h1 align="center">Step 1:</h1>
The first virtual machine created is the Domain Controller which is where Active Directory is created. This virtual machine contains two network adapters, one that connects to the Internet on the outside, and another that connects to the Internal network on the inside that clients will connect to. After the virtual machine is created, Windows Server 2022 is installed and will be assigned an IP address to the Internal network. The external network will automatically be assigned an IP address from the home router (DHCP). 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%201.png?raw=true)

<h1 align="center">Step 2:</h1>
After we assign the IP address, we will name the server and will install an active directory and create our domain. 

