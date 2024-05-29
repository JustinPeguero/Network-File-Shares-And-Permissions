# network-file-shares-and-permissions

<p align="center">
<img src="https://jumpcloud.com/wp-content/uploads/2016/07/AD1.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>
</p>



<h1>Network File Shares and Permissions</h1>
In this tutorial, we will share resources over the network by creating file shares to allow, read, write, or deny access to individual users and groups. <br />

<h2>Enviornments and Technologies Used</h2>

- Microsoft Azure Virtual Machines
- Remote Desktop
- Active Directory Users and Computers
- Network Security Group
- Organization Units

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Windows Server 2019 Datacenter (1809)

<h2>High-Level Steps</h2>

- Create sample file share folders with permissions
- Access file shares as a normal users
- Create an "ACCOUNTANTS" Sccurity Group, assign permissions, and test access

<h2>Actions and Observations</h2>

<h3>Create Sample File Share Folders With Permissions</h3>


![Network File Shares and Permissions stage 1 pic 1](https://github.com/JustinPeguero/Network-File-Shares-And-Permissions/assets/170198869/30eb30ba-9665-4b70-87b5-b5f8ed170074)

</p>
<p>
Create 2 instances of your remote desktop and log into the domain controller as an admin and your client PC as one of the users.
</p>
<br />


![image](https://github.com/JustinPeguero/Network-File-Shares-And-Permissions/assets/170198869/d2a67b3b-ea8e-40f3-bdb5-2232058a41fc)

</p>
<p>
From your domain controller click on the Windows Explorer icon on your taskbar-->This PC-->Click on your C:\ drive to open its contents.
</p>
<br />


![image](https://github.com/JustinPeguero/Network-File-Shares-And-Permissions/assets/170198869/26384a69-3634-4f72-b5a0-9a0f9321f3c3)

</p>
<p>
From your domain controller in the C:\ drive create 4 folders: "read-access", "write-access", "no-access", and "accounting".
</p>
<br />

![image](https://github.com/JustinPeguero/Network-File-Shares-And-Permissions/assets/170198869/04cb43cc-668d-4da4-874e-565692481790)

</p>
<p>
In Windows C:\ drive right click the folder-->hover to Properties-->Click on the Sharing Tab-->Click on Share from the Sharing tab-->Type Domain Users in the bar above the name and permission level. 

There will be a drop down menu that will allow you to select the permission level for your domain users.  Check "Read" for the read-access folder, "Read/Write" for the write-access folder. Instead of adding domain users in the no-access folder, we will use domain admins instead and provide them with "Read/Write" access.  This will give normal users no access to that folder. 

We will go to the client PC and check folders for access in the following steps.
</p>
<br />

![image](https://github.com/JustinPeguero/Network-File-Shares-And-Permissions/assets/170198869/1a0b5c8c-3d09-40f1-9682-f6a4d680efdd)

</p>
<p>
Once your permissions are set there, you can send  and email of that shared folder or share the link into another app.  In the individual items section, there will be a file path that you can copy and paste in a windows explorer search box that will take you to that specific folder.
</p>
<br />

![image](https://github.com/JustinPeguero/Network-File-Shares-And-Permissions/assets/170198869/10ab4e17-ab4d-45a5-9960-f77bbf068d74)

</p>
<p>
Open each folder and create a text document that we can test for access when we log into the client virtual machine as a domain user.  To create the document, right click on each folder-->hover to New-->hover to text document and click.
</p>
<br />

![image](https://github.com/JustinPeguero/Network-File-Shares-And-Permissions/assets/170198869/b0b1bfa2-321f-4a6f-a610-9b7fe87e94f3)

</p>
<p>
Once your file is created, type a sample text, go to File-->Save As-->Name your file-->Click Ok.
</p>
<br />

<h3>Attempt to access file shares as a normal user</h3>

![image](https://github.com/JustinPeguero/Network-File-Shares-And-Permissions/assets/170198869/8e866410-131c-4d0f-a257-b1476f1fb700)

</p>
<p>
On Client-1, navigate to the shared by typing Run in the search bar-->type \\DC-1-->The network folder should populate in a new window.
</p>
<br />

![image](https://github.com/JustinPeguero/Network-File-Shares-And-Permissions/assets/170198869/fb569c16-9f14-4ed0-9606-206999a1784c)

</p>
<p>
Open the read-access folder-->Open your test file-->Attempt to edit the text and save the document. A dialog box will show that you have read access only.
</p>
<br />

![image](https://github.com/JustinPeguero/Network-File-Shares-And-Permissions/assets/170198869/9409c4ba-ea6b-4866-bc46-5e3e39f4d0f8)

</p>
<p>
Open the no-access folder.  Upon clicking you will get a network error stating that you do not have access to this folder.
</p>
<br />

<h3>Create an "ACCOUNTANTS" Security Group, assign permissions, and test access</h3>

![image](https://github.com/JustinPeguero/Network-File-Shares-And-Permissions/assets/170198869/b619f278-8535-4d12-9984-f35f2a0ed66a)

</p>
<p>
Go to DC-1 in Active Directory and create a organization unit _SECURITY_GROUP  then add the group  "ACCOUNTANTS" to that folder.
</p>
<br />

![image](https://github.com/JustinPeguero/Network-File-Shares-And-Permissions/assets/170198869/ec1c0030-65e6-4496-afd7-b228631abb78)

</p>
<p>
Create a security group "ACCOUNTANTS"  in your organizational folder. Right click _SECRUITY_GROUP-->hover New-->hover to Group and click-->Type ACCOUNTANTS in the dialog box for group name-->click on the radio buttons global for group scope and security for group type-->Click Ok
</p>
<br />

![image](https://github.com/JustinPeguero/Network-File-Shares-And-Permissions/assets/170198869/1b28e7c2-5f8d-4049-b6b6-9dc44cf4ceb4)

</p>
<p>
On the "accounting" folder that was created earlier in DC-1 virtual machine, we are going to set the following permissions, for the "accounting folder, add the security group "ACCOUNTANTS" from the properties sharing tab.  Give the group permission read/write permissions. Click on share.
</p>
<br />

![image](https://github.com/JustinPeguero/Network-File-Shares-And-Permissions/assets/170198869/96fc6d87-a089-42a3-8e03-52a2ea5db8da)

</p>
<p>
On Client-1 virtual machine as a user, open Windows File Explorer-->Type\\DC-1 in the file location bar-->Click on the "accounting" folder to access the file.  

An error message shows no access.  The current user does not have access to the file folder. In the next step, we will go back to DC-1 virtual machine, and add the user to the security group for access to that folder.
</p>
<br />

![image](https://github.com/JustinPeguero/Network-File-Shares-And-Permissions/assets/170198869/11ee07dc-530d-4852-bd7f-33e7ba1a5885)

![image](https://github.com/JustinPeguero/Network-File-Shares-And-Permissions/assets/170198869/0d7b79fc-bf9b-42b6-ae24-b24f80b64bd7)

</p>
<p>
On DC-1 virtual machine, add the user to the "ACCOUNTANTS" -->Click on _SECURITY_GROUPS-->Right click "ACCOUNTANTS"-->Click Properties-->Click on Members tab-->Click Add...-->Type the name of the user names in the object box-->Click Find Names-->When the user has been found in your directory, click Ok.
</p>
<br />

![image](https://github.com/JustinPeguero/Network-File-Shares-And-Permissions/assets/170198869/744751fc-646e-4b61-b6cf-6908aae8828d)

</p>
<p>
On the Client-1 virtual machine, click on Start-->click on the user-->click on Sign out to log off the virtual machine. 

You will need to log off and on for the changes to take effect.
</p>
<br />

![image](https://github.com/JustinPeguero/Network-File-Shares-And-Permissions/assets/170198869/09e6de97-3fa3-4c98-8cb2-2b1da70a43e2)

</p>
<p>
Log into your Client-1 virtual machine with your user credentials-->Open Windows File Explorer-->Type\\DC-1 in the file directory bar-->Click "accounting"-->Open the test file.  

*If everything was done correctly, the file should open, and you should be able to edit the document and save it in the network folder.
</p>
<br />
