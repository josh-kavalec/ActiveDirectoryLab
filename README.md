# Active Directory Lab
This project documents the creation of a fully functional Active Directory home lab using Oracle VirtualBox. The environment consists of a Windows Server 2022 domain controller and a Windows 11 client connected through an isolated virtual network. The lab demonstrates the deployment and configuration of Active Directory Domain Services (AD DS), DNS, DHCP, RAS/NAT, and PowerShell automation to simulate a small enterprise environment. 

# Environments and Utilities Used
- Oracle VirtualBox
- Windows Server 2022
- Windows 11
- PowerShell

<h1 align="center">Project Overview: Network Diagram</h1>

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Full%20Diagram.png?raw=true)

# Step 1:
The first virtual machine created is the Domain Controller which is where Active Directory is created. This virtual machine contains two network adapters, one that connects to the Internet on the outside, and another that connects to the Internal network on the inside that clients will connect to. After the virtual machine is created, Windows Server 2022 is installed and will be assigned an IP address to the Internal network. The external network will automatically be assigned an IP address from the home router (DHCP). 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%201.png?raw=true)

# Step 2:
After we assign the IP address, we will name the server and will install an active directory and create our domain. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%202.png?raw=true)

# Step 3:
We are then going to configure NAT and Routing so that clients on the internal network will be able to access the internet through the Domain Controller. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%203.png?raw=true)

# Step 4:
Next we’re going to set up DHCP on the Domain Controller so when we create a Windows 11 machine it will automatically be assigned an IP Address. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%204.png?raw=true)

# Step 5:
Before we create our client virtual machine, the final thing we do in the Domain Controller is we’re going to run a PowerShell script that will automatically create a thousand users in Active Directory. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshopt%205.png?raw=true)

# Step 6:
After creating the users, we’re going to create another virtual machine and install Windows 11 and that virtual machine will be connected to the private VirtualBox network. We will name that machine Client 1 and join it to the domain. We will then log in with one of the domain accounts.

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%206.png?raw=true)

<h1 align="center">Step-by-Step Project Walkthrough</h1>

We created our first virtual machine labeled “Domain Controller” in which I currently have Windows Server 2022 Installed. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%207.png?raw=true)

We will then proceed to configure the virtual machine labeled “Domain Controller.” Clicking on Settings, and clicking onto the Network tab, we can see that we currently have one Network Adapter connected. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%208.png?raw=true)

Based on the Network Diagram previously listed, we have two network adapters connected to the Domain Controller. We must select Adapter Two and Enable Network Adapter. Next to the “Attached to” dropdown, we will select Internal Network. This is because we already have one dedicated for the Internet, and now we have one for our Internal Network. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%209.png?raw=true)

Once we are logged into the Windows Server 2022, we will enter the Administrator password to login. (I had created one prior) 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%2010.png?raw=true)

For the two Network Adaptors connected to the Domain Controller, we know that the Network Adapter connected to the Internet (Outside Network) will automatically be assigned an IP address from the home router. For the Internal Network Adapter, we must set it up individually. We will access the Network & Internet Settings, and click on Change adapter options.

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%2011.png?raw=true)

Here we will see two Ethernet Network connections. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%2012.png?raw=true)

With these two Ethernet Network connections we know that one is for our Internet and one is for the Internal Network. In order to find out which is the Internet, and which is the Internal Network, we will right click on the Ethernet Connection, click Status, click Details, and look at the IP Address assigned. The connection labeled Ethernet has an IPv4 address of 10.0.2.15 which is a more typical IP address to be connected to the Internet. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%2013.png?raw=true)

The connection labeled Ethernet 2 is going to represent out Internal network due to having an IPv4 address of 169.254.94.176

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%2014.png?raw=true)

For routing purposes later down the road, we will rename both Ethernet Connections to their rightful network. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%2015.png?raw=true)

We will then right click on the Internal Network, select Properties

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%2016.png?raw=true)

Select Internet Protocol Version 4 (TCP/IPv6)

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%2017.png?raw=true)


We will then set the IP address of the Internal Network that is stated in the previous Diagram:
- IP address: 172.16.0.1
- Subnet Mask: 255.255.255.0
- Default Gateway: (leave empty) 
- Preferred DNS server: 127.0.0.1 (loopback) 
 
![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%2018.png?raw=true)

Once this is completed, we can click OK and exit the Network & Internet Settings. The next step is to rename the PC. We will do this by right clicking on the Start Menu and selecting System.

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%2019.png?raw=true)

Select “Rename this PC” 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%2020.png?raw=true)

We will rename this PC “DC” which is short for Domain Controller. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%2021.png?raw=true)


After doing so, we will restart the Virtual Machine. 
