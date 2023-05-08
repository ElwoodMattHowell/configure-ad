<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Set up resources in Azure
- Install Active Directory
- Create an Admin and normal User account in Active Directory
- Join client machine to domain
- Set up Remote Desktop for non-administrative users on client machine
- Create additional users and log in to client machine with created users

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


Our first step will be to set up our resources in Azure.  We need to create the Domaine Controller virtual machine using a Windows Server Image.  Once our Domaine Controller(DC) has been created, we will set the DC's NIC private IP address to be static.  Next we will create our client machine using a Windows 10 image.  Be sure to use the same Resource Group and Vnet you used when setting up the Domaine Controller.
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


Now we will install Active Directory Domain Services on our Domaine Controller.  Using Microsoft Remote Desktop, login to your Domaine Controller.  Server Manager should be open when you login.  If not, search Server Manager and open.  In Server Manager click _Add roles and Features_.  Click through to _Select server roles_ and check the box next to _Active Directory Domain Services_.  Click _Add Features_, click through to _Install_ and install.  When Active Directory Domaine Services has been installed click _Close_.  In the upper right hand corner of your screen, you should see a flag with a yellow warning sign,  click on that warning sign and the click _Promote this server to a domain controller_.  Clcik the circle next to _Add a new forest_ and enter a Root domaine name.  It is a private domain, so you can name it as you wish but it must be in the form of _example.com_.  Click _Next_ and enter a password of your choice.  Click through to _Install_ and install.  Once Active Directory is installed, your computer will restart.  When you log back in, you will use _mydomain.com\your-user-name_ as your username.  
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
