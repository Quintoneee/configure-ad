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
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
