# Active Directory Lab
This project documents the creation of a fully functional Active Directory home lab using Oracle VirtualBox. The environment consists of a Windows Server 2022 domain controller and a Windows 11 client connected through an isolated virtual network. The lab demonstrates the deployment and configuration of Active Directory Domain Services (AD DS), DNS, DHCP, RAS/NAT, and PowerShell automation to simulate a small enterprise environment. 

# Environments and Utilities Used
- Oracle VirtualBox
- Windows Server 2022
- Windows 11
- PowerShell

# Project Overview: 
<h1 align="center">Network Diagram</h1>

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

<h1 align="center">Step 1 Walkthrough:</h1>

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

<h1 align="center">Step 2 Walkthrough:</h1> 

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

<h1 align="center">Step 3 Walkthrough:</h1>

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

<h1 align="center">Step 4 Walkthrough:</h1>

The next step in our Network Diagram is to set up the DHCP Server on our Domain Controller. This will allow our Windows 11 Clients to get an IP address which will allow them to connect to the Internet even though they will be on their own Private Network. 

To set up DHCP, we will go back to the Server Manager Dashboard. Click Add roles and Features. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/53.png?raw=true)

Select Next through Before you Begin, Installation Type, and Server Selection. Under Server Roles, select DHCP Server. Click Next

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/54.png?raw=true)

Continue to click Next, and then click Install.

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/55.png?raw=true)

Once Installed we can return to the Server Manager Dashboard. 

From here we will click on Tools in the top right corner and Select DHCP. Here we will set up our scope. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/56.png?raw=true)

The purpose of DHCP is to allow the computers on the network to be automatically assigned an IP address. Looking at our Network Diagram, we will configure DHCP based on the following: 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/Active%20Directory%20Screenshot%204.png?raw=true)

We will click the arrow next to dc.mydomain.com
Notice how we have both IPv4 and IPv6 with red errors indicating they are not yet up and running. We will right click on IPv4 and select New Scope. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/57.png?raw=true)

For the Scope Name, we are going to name it after the IP range listed in the Network Diagram. Click Next.

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/58.png?raw=true)

We will then insert the Start/End IP addresses. We will also insert the Subnet Mask based on our Network Diagram as 255.255.255.0
Click Next

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/59.png?raw=true)

Click Next through Add Exclusions and Delay. Under Lease Duration, for our Virtual Machine purpose, I will increase the duration to 365 days. Click Next. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/60.png?raw=true)

Under Configure DHCP Options, select “Yes, I want to configure these options now” and click Next. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/61.png?raw=true)

Since we configured NAT on the Domain Controller and it has Routing configured, it will forward traffic from the clients to the Internet. Because of this, the clients are able to use the Internal Network Adapter of the Domain Controller as their Default Gateway/ Router. For our DHCP configuration, we will enter the Domain Controller’s IP address under Router (Default Gateway). Make sure to click Add before clicking Next. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/62.png?raw=true)

Since we installed Active Directory on the Domain Controller, it automatically installed the Domain Name System (DNS). Because of this, we are going to use the Domain Controller as our DNS Server. 
Under Domain Name and DNS Server, select Next. 
 
![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/63.png?raw=true)

Click Next through WINS Server, then select “Yes, I want to activate this scope now” under Activate Scope. Click Next. Click Finish. 
To make sure DHCP is up in running we will right click on dc.domain.com and select Authorize. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/64.png?raw=true)

Then right click on dc.domain.com again and select Refresh.

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/65.png?raw=true)

We can now see that our IPv4 and IPv6 have turned green which indicates that our DNS is now set up. You may also notice that the Scope is set up as well. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/66.png?raw=true)

<h1 align="center">Step 5 Walkthrough:</h1>

Now that we have our DNS configured, our next step is to use our PowerShell script to create 1,000 sample users and create our client computer. Before moving forward, for the purpose of this project we are going to make a configuration that will allow us to browse the Internet on the Virtual Machine. Typically we would not do this in a production environment, but for the lab we will do the configuration. 

In the Server Manager Dashboard, we are going to click on Configure this local server. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/67.png?raw=true)

Under the Local Server we are going to click on the IE Enhanced Security Configuration. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/68.png?raw=true)

We will select Off for both Administrators and Users. Click OK.

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/69.png?raw=true)

We will then open Microsoft Edge (or another Internet browser) and paste this link. This link is a .zip file that contains the names of the users we will create using PowerShell. 

https://github.com/joshmadakor1/AD_PS/archive/master.zip

Once the link is entered, the .zip file will appear under Downloads. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/70.png?raw=true)

We will then save AD_PS-master.zip on our Desktop. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/71.png?raw=true)

In this folder, we have a file titled “names” which is a list of randomly generated first and last names. These will be the 1,000 users we will add using our PowerShell script. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/72.png?raw=true)

We will then add the user that we had previously created. In this case, John Smith.

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/73.png?raw=true)

We will click Windows Start, Select Windows Powershell, scroll down to Windows PowerShell ISE, right click and select More, and click Run as administrator.

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/74.png?raw=true)

Once Windows PowerShell ISE is open, select the folder icon (Open Script) in the top left corner. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/75.png?raw=true)

We will select the folder we saved to our Desktop (AD_PS-master) and select the PowerShell script titled “1_CREATE_USERS”. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/76.png?raw=true)

The script should now appear Within Windows PowerShell ISE.

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/77.png?raw=true)

If we run this script, we receive an error. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/78.png?raw=true)

This is a security feature, but since we are in a closed environment, we are going to un-restrict the execution policy. Within the script we will write the following: 

Set-ExecutionPolicy Unrestricted

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/79.png?raw=true)

An Execution Policy Change window will appear and we will select “Yes to All”. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/80.png?raw=true)

Before we run this script, we have to go to the actual directory where the script is. We are going to change the directory and select the user which we are logged in as. In this example, it is a-jsmith. The script was saved on the Desktop and we selected the file where the script is. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/81.png?raw=true)

If we list the directory (ls), we can see the names.txt from the script.

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/82.png?raw=true)

We will then select Run Script and select “Run once”. As we run the script, we can see the new users being created. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/83.png?raw=true)

If we open Active Directory, we can now see all the new users created. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/84.png?raw=true)

If we also go under Find Users, Contacts, and Groups we are able to find the user that we previously created. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/85.png?raw=true)

<h1 align="center">Step 6 Walkthrough:</h1>

Now that all of the users are created and our whole environment is set up, our last step based on the Network Diagram is to create the Windows 11 Virtual Machine in VirtualBox. This Virtual Machine is going to use an Internal Network Adapter and should get an IP address from the DHCP Server we configured and verify after the fact. (Make sure you use Windows 11 Pro)

Now we have created our new Virtual Machine and named it Client: 1.
 
![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/86.png?raw=true)

Under our Client 1 Network Settings, instead of using NAT as our Network Adapter and connecting to our home network, I will change this to Internal Network since we configured our Client 1 user to use the Internal Network. This will allow us to get a DHCP address from the Domain Controller to emulate a corporate network. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/87.png?raw=true)

For the Client: 1 Virtual Machine we are going to name this local computer User. (You can click Next on Password)

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/88.png?raw=true)

Once logged into the Client: 1 Windows 11 Pro, we will open up the Command Prompt. We will use the command ipconfig to show us the IP address, Subnet Mask, and Default Gateway. We will notice that the DNS Suffix is mydomain.com which shows our Active Directory domain. (Make sure you have Domain Controller Virtual Machine running) 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/89.png?raw=true)

In the Command Prompt we will try to ping something on the internet. For Example, we will enter ping www.google.com 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/90.png?raw=true)

Since we can ping the Internet, this means that our whole infrastructure (based on our Network Diagram) is set up correctly. We have connectivity all the way to the Default Gateway (which is the Domain Controller) and the Domain Controller is properly forwarding it out to the Internet. 

Next we are going to enter ping mydomain.com which is our Domain Controller (make sure you have the Domain Controller Virtual Machine running) 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/91.png?raw=true)

Before we do anything with our client computer, let's rename it. Right click the Start menu and select System. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/92.png?raw=true)

Instead of clicking “Rename this PC” we are going to scroll down to Advanced System Settings because we can join the domain at the same time. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/93.png?raw=true)

Select Computer name in System Properties and select Change. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/94.png?raw=true)

We will rename the computer name to CLIENT1. We will select Domain and enter mydomain.com and click OK. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/95.png?raw=true)

Under Computer Name/ Domain Changes we will enter the credentials of the Administer Account we created. In this example mine was a-jsmith and the password I created. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/96.png?raw=true)

Once the credentials are entered and approved, restart the machine. 

If we go back to our Domain Controller, select Start > Windows Administrative Tools > Active Directory Users and Computers.

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/97.png?raw=true)

If we select Computers, we can now see that CLIENT1 is a member of the domain.

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/98.png?raw=true)

Once the Client 1 machine is restarted, instead of logging in to the local user that we created, select Other user. Notice under the log in credentials we see “Sign in to: MYDOMAIN”. We can sign in to one of the user accounts we created earlier. In this case, my user jsmith. 

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/99.png?raw=true)

If we open our command prompt and enter whoami, we can see the user we created. If we enter ipconfig /all we can see that we are connected to mydomain.com

![image alt](https://github.com/josh-kavalec/ActiveDirectoryLab/blob/main/100.png?raw=true)

# What I Learned: 

This project successfully demonstrated the deployment and configuration of a functional Active Directory environment within a virtualized home lab using Oracle VirtualBox. By implementing a Windows Server 2022 domain controller and a Windows 11 client, I gained hands-on experience configuring essential enterprise services, including Active Directory Domain Services (AD DS), DNS, DHCP, and RAS/NAT. I also used PowerShell to automate user account creation, reinforcing the importance of scripting and automation in systems administration.

Completing this project strengthened my understanding of Windows Server administration, domain management, user and group administration, network services, and virtualization. It also provided practical experience troubleshooting connectivity, authentication, and configuration issues commonly encountered in enterprise environments.

Overall, this home lab simulates a real-world IT infrastructure and demonstrates my ability to plan, deploy, configure, and manage a Windows Active Directory environment. The knowledge and skills gained through this project provide a strong foundation for roles in IT support, systems administration, and cybersecurity while preparing me for more advanced enterprise networking and security projects.
