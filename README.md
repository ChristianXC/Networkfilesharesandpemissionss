
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Network Fileshares And Permissions </h1>
This tutorial outlines the implementation of network and file share permissions within Azure Virtual Machines. I will demonstrate sharing documents within the network and assigning read/write permissions to certain people or groups. <br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Active Directory Domain Services


<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1 - Create some sample file shares with various permissions.

- Step 2 - Attempt to access file shares as a normal user.
  
- Step 3 - Create a Security Group, assign permissions, and test access.



<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/zVDBwWC.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
<p>
Sign in to your domain controller and general user account.
</p>
<br />

<p>
<img src="https://i.imgur.com/rhpmpEJ.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
<p>
On the domain controllers C:\ drive, create 4 folders: “read-access”, “write-access”, “no-access”, “accounting”.

</p>
<br />

<p>
<img src="https://i.imgur.com/dTYIW7b.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
<p>
Right-click the _ReadAccess folder, click properties, click sharing then share and type domain users and give them read access; repeat the process for the _WriteAccess folder but give them read/write access instead.
</p>
<br />

<p>
<img src="https://i.imgur.com/IrQQQpV.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
<p>
For the _NoAccess folder repeat the same process but give domain "ADMINS" read/write access by simply typing "domain admins" in the search bar.
</p>
<br />

<p>
<img src="https://i.imgur.com/U3Rkj4H.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
<p>
Switch from the domain controller to the general user, go to File Explorer, and enter your domain controller's name in the search bar. You will see that you have access to read and write folders as a domain user but nothing else. We're going to change that by giving our "general user" accountant permissions.
</p>
<br />

<p>
<img src="https://i.imgur.com/JcUdlkN.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
<p>
So we're back to our domain controller now, click the Windows icon go to "Windows Administrative Tools">" Active Directory Users And Computers" and create an organizational unit called _groups. Inside the group, we'll create a security group called "Accountants" by right-clicking inside _group clicking new then group. 
</p>
<br />

<p>
<img src="https://i.imgur.com/zQtBZXC.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
<p>
We'll then go back to our C:\ drive where we created the accounting folder and right-click accountants, click properties>sharing>share enter in the search bar accountants, and assign them read/write permissions. 
</p>
<br />

<p>
<img src="https://i.imgur.com/q7HaXT4.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
<p>
From there, we go back to active directory users and computers and we'll assign our "general user" accountant permissions. Find that group we created with accountants in it>double-click accountants>click members>add>type the user you want to add>click ok>apply.
</p>
<br />

<p>
<img src="https://i.imgur.com/2WZPQ3E.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Refresh the domain controller as well as our "general user (now accountant)" go back to File Explorer try to access the once inaccessible accounting folder and observe it works. :)
</p>
<br />
