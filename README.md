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
- Ensure connectivity between Domaine Controller and client machine
- Install Active Directory
- Create an Admin and normal User account in Active Directory
- Join client machine to domain
- Set up Remote Desktop for non-administrative users on client machine
- Create additional users and log in to client machine with created users

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


Our first step will be to set up our resources in Azure.  We need to create the Domain Controller virtual machine using a Windows Server Image.  Once our Domain Controller(DC) has been created, we will set the DC's NIC private IP address to be static.  Next we will create our client machine using a Windows 10 image.  Be sure to use the same Resource Group and Vnet you used when setting up the Domain Controller.
<br />


<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


Our next step will be to ensure connectivity between our Domain Controller and our client machine,  We must enable ICMPv4 on the local Windows firewall of our Domain Controller.  Login to our Domain Controller, and type _Firewall_ in the search box.  Click on _Windows Defender Firewall with Advanced Security_.  In the upper left hand corner, click on _Inbound Rules_.  Click on the header of the Protocol column.  This will group rules by protocol.  Enable all ICMPv4 rules by clicking on the rule and clicking _Enable_ in the panel to the right.  Close when finished.

<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


Now we will install Active Directory Domain Services on our Domain Controller.  Using Microsoft Remote Desktop, login to your Domain Controller.  Server Manager should be open when we login.  If not, search Server Manager and open.  In Server Manager click _Add roles and Features_.  Click through to _Select server roles_ and check the box next to _Active Directory Domain Services_.  Click _Add Features_, click through to _Install_ and install.  When Active Directory Domain Services has been installed click _Close_.  In the upper right hand corner of our screen, we should see a flag with a yellow warning sign,  click on that warning sign and the click _Promote this server to a domain controller_.  Click the circle next to _Add a new forest_ and enter a Root domain name.  It is a private domain, so we can name it as we wish but it must be in the form of _example.com_.  Click _Next_ and enter a password of your choice.  Click through to _Install_ and install.  Once Active Directory is installed, our computer will restart.  When we log back in, we will use _root-domain-name\user-name_ as our username.  
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


Now that we have Active Directory installed, we will create two accounts; an Admin account and a User account.  In the search bar, type _Active Directory Users and Computers_ and click on that selection.  In the panel to the right, you should see the Root domain name you selected in the previous step.  Right click on that, click _New_, and then _Organizational Unit_.  For the purposes of this exercise, we will call this organizational unit EMPLOYEES.  Click _Okay_ and repeat the process, creating an organizational unit called _ADMINS_.  Next right click on _ADMINS_, click on _New_, and then _User_.  We will create a new admin account.  You can choose the name and logon name of your choice.  Click _Next_ and choose a password for your admin user.  For our purposes we will uncheck the box next to _User must change password at next logon_, but it is generally a best practice to keep that checked.  Click _Next_, and _Finish_.  Now we have to actually add the newly created user as a Domain Administrator.  In the Admins folder, right click on the user you just created and click _Properties_.  Click the _Member Of_ tab and click _Add_.  Type _domain_, click _Check Names_, click _Domain Admins_, click, _OK_, _OK_, _Apply_, and _OK_.  Log out and log back in using _root-domain-name\user-just-created_ as your username.
<br />


<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


Our next step will be to connect or client machine to our Domain Controller.
<br />
