<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This Project outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Set up Domain Controller and Client 1 in Azure
- Install Active Directory and create a Domain Admin user within the Domain
- Join Client 1 to your Domain
- Set up Remote Desktop for non-administrative users on Client-1 and create a bunch of additional users 
- Dealing with Account Lockouts


<h2>Deployment and Configuration Steps</h2>

<h4> Setup Domain Controller and Client-1 in Azure:</h4>

<p>
<img src="https://i.imgur.com/mpCWlDp.jpeg" height="50%" width="50%" alt="Domain Controller"/>
</p>
<p>
The first step is to set up a domain controller in Azure. You will create a resource group, a virtual network and subnet, and a domain controller VM in Windows Server 2022 named DC-1. 
</p>
<p>
  <img src="https://i.imgur.com/N5kMX3A.jpeg" height="45%" width="45%" alt="Windows Firewall"/>  <img src="https://i.imgur.com/ITHHpLU.jpeg" height="30%" width="30%" alt="Windows Firewall"/> 
</p>
<p>
  Another thing that we are going to do is go over to the VM Windows settings to get access to the firewall and turn it off so we can test the connectivity. 
</p>
<br />

<p>
<img src="https://i.imgur.com/JdfPOy3.jpeg" height="50%" width="50%" alt="Client-1"/>
</p>
<p>
Now we are going to create a second VM in Windows 10 called Client 1, but make sure to attach it to the same region and virtual network. 
</p>
<p>
  <img src="https://i.imgur.com/zIggtue.jpeg" height="50%" width="50%" alt="Client-1"/>
</p>
<p>
  Still working with Client-1, take the private IP address from the domain controller and set it in Client-1's DNS (domain name server). 
</p>
<br />

<p>
<img src="https://i.imgur.com/yIZZ1sg.jpeg" height="50%" width="50%" alt="Client-1"/>
</p>
<p>
Above, we are going to log Back into Client-1 and open PowerShell so we can ping the private address of the Domain controller, as well as make sure that the ping was successful. 
</p>
<br />

<h4>Install Active Directory and create a Domain Admin user within the Domain:</h4>

<p>
  <img src="https://i.imgur.com/Du4w1tL.jpeg" height="40%" width="40%" alt="Active Directory"/>
  <img src="https://i.imgur.com/ec1t5QR.jpeg" height="40%" width="40%" alt="Active Directory"/>
  <img src="https://i.imgur.com/hFe5E0f.jpeg" height="40%" width="40%" alt="Active Directory"/>
 <img src="https://i.imgur.com/8B2dQd3.jpeg" height="40%" width="40%" alt="Active Directory"/> 
</p>
<p>
  Log in to the Domain Controller. From there, we will be installing Active Directory Domain Services. 
</p>
<br />

<p>
   <img src="https://i.imgur.com/mawECm8.jpeg" height="50%" width="50%" alt="MyDomain.com"/>
</p>
<p>
  Promote as the Domain controller and set up a new forest called mydomain.com. It essentially is whatever you want it to be, just be sure to remember it. Then restart and log back in to the Domain Controller as mydomain.com\whatever username you created. In this case, it would be mydomain.com\quintoneee. 
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
  Create a new employee called Jane Do, and the username is going to be jane_admin. After that, we are going to add Jane_Admin to the Domain Admins Security Group.
</p>
<br />

<h4> Join Client 1 to your Domain:</h4>
<p>
   <img src="https://i.imgur.com/jL6B34A.jpeg" height="40%" width="40%" alt="Client-1"/>
</p>
<p>
  Log in to Client-1 as the original local admin and join it to the domain. The computer will restart when you do this. 
</p>
<br />

<p>
    <img src="https://i.imgur.com/xbh0fhk.jpeg" height="40%" width="40%" alt="Client-1"/>
</p>
<p>
  Log in to the Domain Controller and verify Client-1 shows up in ADUC.
</p>
<br />

<p>
 <img src="https://i.imgur.com/uCjVgU5.jpeg" height="40%" width="40%" alt="Clients unit"/> 
 <img src="https://i.imgur.com/KXArIJp.jpeg" height="40%" width="40%" alt="Clients unit"/>
</p>
<p>
  Create a new OU named “_CLIENTS” and then drag Client-1 into the _CLIENTS folder at the bottom of the screen.
</p>
<br />

<h4>Setup Remote Desktop for non-administrative users on Client-1 and Create a bunch of additional users:</h4>

<p>
  <img src="https://i.imgur.com/aMZKx6j.png" height="40%" width="40%" alt="Non-Administrative users"/>  
</p>
<p>
  Log in to Client-1 as mydomain.com\jane_admin and open the system properties. Select Remote Desktop, then allow domain users access to the remote desktop. Now you can log into Client-1 as a normal, non-administrative user. 
</p>
<br />

<p>
    <img src="https://i.imgur.com/FOKp0HD.jpeg" height="40%" width="40%" alt="Additional Users"/> 
    <img src="https://i.imgur.com/lCZ1ElT.jpeg" height="40%" width="40%" alt="Additional Users"/>  
</p>
<p>
  Log in to DC-1 as Jane_Admin and then open PowerShell_ise as an administrator. 
</p>
<br />

<p>
   <img src="https://i.imgur.com/RvDjLIB.jpeg" height="40%" width="40%" alt="Additional Users"/>
   <img src="https://i.imgur.com/NoPs4hA.jpeg" height="40%" width="40%" alt="Additional Users"/> 
</p>
<p>
  Create a new File and paste the contents of the script in the first photo into it; this is what's going to help create the users. 
</p>
<br />

<p>
   <img src="https://i.imgur.com/2JDoWae.jpeg" height="40%" width="40%" alt="Additional Users"/>
   <img src="https://i.imgur.com/xxMaZA7.png" height="40%" width="40%" alt="Additional Users"/>
</p>
<p>
  Run the script and observe the accounts being created and also When finished, open ADUC and observe the accounts in the appropriate OU　(_EMPLOYEES).
</p>
<br />

<h4>Dealing with Account Lockouts:</h4>

<p>
  <img src="https://i.imgur.com/nmeFuU5.jpeg" height="40%" width="40%" alt="Account Lock outs"/>
</p>
<p>
  Here we just attempted to log in with a random user, and the password failed. This happened a couple of more times, which locked us out of the account. 
</p>
<br />

<p>
  <img src="https://i.imgur.com/DaRjNiP.jpeg" height="40%" width="40%" alt="Account Lock outs"/>
  <img src="https://i.imgur.com/OYwnetT.jpeg" height="40%" width="40%" alt="Account Lock outs"/> 
</p>
<p>
  Go to Active Directory and find the user. Once you're in the user's account, you will see the account is locked. So, we will unlock and reset the password as well. Logging in with that user shouldn't be an issue now. 
</p>
<br />

