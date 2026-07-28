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

# Step 1 Walkthrough: 

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

So far throughout this process we have created a Virtual Machine for our Internet NIC and our Internal NIC in which we assigned it an IP address. We also renamed our PC to DC (short for Domain Controller). 

# Step 2 Walkthrough: 

Our next steps are to install Active Directory Domain Services and create a Domain. To begin, we will start from the Server Manager Dashboard and select Add roles and features. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%2022.png?raw=true)

Under Before You Begin, click Next

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%2023.png?raw=true)

Under Installation Type, make sure that Role-based or feature-based installation is selected. Click Next.

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%2024.png?raw=true)

Under Server Selection, this is going to be the server where we want to install Active Directory Domain Services. Click Next. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%2025.png?raw=true)

Under Server Roles, select Active Directory Domain Services. Click Next

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%2026.png?raw=true)

Under Features, Click Next. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%2027.png?raw=true)

You will Click Next through AD DS and Confirmation and the Click Install. 

Once the installation is complete, Click Close. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/28.png?raw=true)

Notice in the top right of the Server Manager Dashboard, the flag with a yellow exclamation mark. Click on it. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/29.png?raw=true)

Click “Promote this server to a domain controller” 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/30.png?raw=true)

Under Deployment Configuration Select “Add a new Forest” and insert mydomain.com for the Root Domain Name. Click Next.

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/31.png?raw=true)

Under Domain Controller Options, create a Directory Services Restore Mode (DSRM) password, Click Next

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/32.png?raw=true)

Click Next throughout the rest of the Active Directory Domain Services Configuration Wizard until the Install option appears. Click Install.

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/33.png?raw=true)

The computer will automatically restart. Sign back in.

Moving forward, we are now going to create our own dedicated Domain Admin Account rather than using the built-in Administrator account. 
Click the Start icon in the bottom left and select the Windows Administrative Tools folder, and Select Active Directory Users and Computers

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/34.png?raw=true)

With the Active Directory Users and Computers window open, we can see on the left side our newly created domain titled mydomain.com

Next, we will create an Organizational unit to put our Admin account in. We will right click on mydomain.com, select New, and click Organizational Unit.

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/35.png?raw=true)

We can think of this as a folder in Active Directory. We will name this _ADMINS and then Click OK. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/36.png?raw=true)

We will create a new user by right clicking on _ADMINS, select New, and Click User. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/37.png?raw=true)

For this example, we will create the User John Smith. For the User logon name, we will use a-jsmith to signify that this is an admin account for John Smith. 
 
![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/38.png?raw=true)

We will then create a password for the User account. I disabled “User must change password at next logon” and selected “Password never expires” due to this being in a lab environment.

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/39.png?raw=true)

Select Next, and then Finish.

You’ll notice we have our account set up under _ADMINS, but it is not an Admin yet even though we named it a-jsmith. 

To make a Domain Admin, we will right click on the User, and Select Properties

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/40.png?raw=true)

Then Select Member Of
 
![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/41.png?raw=true)

Select Add

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/42.png?raw=true)

Under “Enter the object names to select” we will input domain admins. We will then select Check Names.
 
![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/43.png?raw=true)

Select OK, and click Apply, and then click OK again. 

Now we have our very own Domain Admin account. To use this, we will then Sign out of the Domain Controller. 

Instead of signing in to the Administrator, we will select other user. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/44.png?raw=true)

Under the Other user sign in, we can see “Sign in to: MYDOMAIN”

We are going to use our Domain Admin account we previously created. The User I created, John Smith:

- Username: a-jsmith
- Password: The password you created for the User

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/45.png?raw=true)

# Step 3 Walkthrough: 

Looking Back on our Network Diagram, the next step is to install the Remote Access Service (RAS)/ Network Address Translation (NAT). The purpose of this step is when we create our Windows 11 client, it will allow the client to be on a Private Virtual Network, but still have access to the Internet through the Domain Controller. 

To do this, under the Server Manager Dashboard, we will select Add roles and features. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/46.png?raw=true)

Select Next through Before you Begin, Installation Type, and Server Selection. Under Server Roles, we will enable Remote Access which is the role we need to install. Click Next

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/47.png?raw=true)

Click Next under Features. 

Under Roles features, we are going to install Routing. Once enabled, DirectAccess and VPN (RAS) will also be automatically selected. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/48.png?raw=true)

Continue to Click Next, then Install.

After the installation we will close out the Add Roles and Features Wizard. From the Server Manager Dashboard, we will select Tools in the right-hand corner and select Routing and Remote Access.

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/49.png?raw=true)

We will right click on our Domain Controller (DC) local and select Configure and Enable Routing and Remote Access.

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/50.png?raw=true)

We will click Next. Under Configuration, we will select Network Address Translation (NAT) which will allow internal clients to connect to the Internet using one public IP address. Then click Next. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/51.png?raw=true)

Under NAT Internet Connection, select the Network Interface “Internet” which we had previously renamed. Then click Next. Click Finish. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/52.png?raw=true)

We have now configured both the Remote Access Service (RAS) and Network Address Translation (NAT). Since this is completed, once we create our Windows 11 clients, they should be able to connect to the Internet. 

# Step 4 Walkthrough:
