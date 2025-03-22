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

- Setup Domain Controller and Client 1 in Azure
- Install Active Directory and create a Domain Admin user within the Domain
- Join Client 1 to your Domain
- Setup Remote Desktop for non-administrative users on Client-1 and Create a bunch of additional users and attempt to log into client-1 with one of the users
- Dealing with Account Lockouts and Enabling and Disabling Accounts


<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/mpCWlDp.jpeg" height="50%" width="50%" alt="Domain Controller"/>
</p>
<p>
The first step is to setup a domain controller in Azure. You will create a resource group, a virtual network and subnet, and domain controller vm in windows server 2022 named DC-1. 
</p>
<p>
  <img src="https://i.imgur.com/N5kMX3A.jpeg" height="45%" width="45%" alt="Windows Firewall"/>  <img src="https://i.imgur.com/ITHHpLU.jpeg" height="30%" width="30%" alt="Windows Firewall"/> 
</p>
<p>
  Another thing that we are going to do is go over to the VM windows settings to get access to the firewall and turn it off so we can test the conectivity. 
</p>
<br />

<p>
<img src="https://i.imgur.com/JdfPOy3.jpeg" height="50%" width="50%" alt="Client-1"/>
</p>
<p>
Now we are going to create a second VM in windows 10 called Client 1, but make sure to attatch it to the same region and virtual network. 
</p>
<p>
  <img src="https://i.imgur.com/zIggtue.jpeg" height="50%" width="50%" alt="Client-1"/>
</p>
<p>
  Still working with Client-1, take the private ip address from the domain controller and set it in client 1 DNS (domain name server). 
</p>
<br />

<p>
<img src="https://i.imgur.com/yIZZ1sg.jpeg" height="50%" width="50%" alt="Client-1"/>
</p>
<p>
Above we are going to log Back into Client-1 and open powershell so we can ping the private address of the Domain controller, as well as make sure that the ping was successful. 
</p>
<br />

<p>
  <img src="https://i.imgur.com/Du4w1tL.jpeg" height="40%" width="40%" alt="Active Directory"/>
  <img src="https://i.imgur.com/ec1t5QR.jpeg" height="40%" width="40%" alt="Active Directory"/>
  <img src="https://i.imgur.com/hFe5E0f.jpeg" height="40%" width="40%" alt="Active Directory"/>
 <img src="https://i.imgur.com/8B2dQd3.jpeg" height="40%" width="40%" alt="Active Directory"/> 
</p>
<p>
  Login into the Domain Controller. From there we will be installing Active Directory Domain Services. 
</p>
<br />

<p>
   <img src="https://i.imgur.com/mawECm8.jpeg" height="50%" width="50%" alt="MyDomain.com"/>
</p>
<p>
  Promote as the Domain controller and setup a new forest called mydomain.com. It essentially be whatever you want it to be, just be sure to rememeber it. Then restart and log back in to the Domain Controller as mydomain.com\ whatever username you created. In this case it would be mydomain.com\quintoneee. 
</p>
<br />

<p>
 <img src="https://i.imgur.com/sa7H5wl.jpeg" height="40%" width="40%" alt="Organizational unit"/> 
 <img src="https://i.imgur.com/Hikn39D.jpeg" height="40%" width="40%" alt="Oragnizational Unit"/>
</p>
<p>
  In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”. 
</p>
<br />

<p>
   <img src="https://i.imgur.com/mtEjaeV.jpeg" height="40%" width="40%" alt="ADMINS unit"/> 
</p>
<p>
  We are going to go to the ADUC and create a new OU named “_ADMINS”.
</p>
<br />

<p>
  <img src="https://i.imgur.com/DMDQ0QZ.png" height="40%" width="40%" alt="Creating Employee"/>
  <img src="https://i.imgur.com/OSSrNdK.png" height="40%" width="40%" alt="Creating Employee"/>
</p>
<p>
  Create a new emplyee called Jane Doe and the username is going to be jane_admin. After that we are going to add jane_admin to the Domain Admins Security Group.
</p>
<br />

<p>
   <img src="https://i.imgur.com/jL6B34A.jpeg" height="40%" width="40%" alt="Client-1"/>
</p>
<p>
  Login to Client-1 as the original local admin and join it to the domain. Computer will restart when you do this. 
</p>
<br />

<p>
    <img src="https://i.imgur.com/xbh0fhk.jpeg" height="40%" width="40%" alt="Client-1"/>
</p>
<p>
  Login to the Domain Controller and verify Client-1 shows up in ADUC.
</p>
<br />

<p>
 <img src="https://i.imgur.com/uCjVgU5.jpeg" height="40%" width="40%" alt="Clients unit"/> 
 <img src="https://i.imgur.com/KXArIJp.jpeg" height="40%" width="40%" alt="Clients unit"/>
</p>
<p>
  Create a new OU named “_CLIENTS” and then drag Client-1 into the _CLIENTS folder at the bottom of the screen.
</p>
