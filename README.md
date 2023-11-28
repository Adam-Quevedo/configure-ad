<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial covers how to set up a Active Directory inside a Virtual Machine using Azure.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computer)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Virtual Machine Configuration</h2>

<p>

Before we can do anything regarding Active Directory we need to set up our Virtual Machines, one as a Domain Controller and the other a client.
Using and Azure subscription we can create just thoose things. 

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/98a3cf01-dbfd-4f41-8834-f8853b0ac3fc)

After creating both of the Virtual Machines on the same Virtual Network we can now change the private IP Address of the DomainC VM to Static on the NIC Card.

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/49953d12-6127-42d9-8c10-de4f36b4a5df)

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/58964bc8-6378-4c32-8747-0b4e53ecde88)

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/41d29110-0b0c-40d1-9987-4aa9d6cee998)

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/765a1dce-5071-4806-b03d-6d7fc4f11f62)

<br/> 

Once everything is connected we can now Remote Desktop into the Domain Controller to change the ICMPv4 settings.

<h2>Active Directory Configuration</h2>

<br/> 

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/0d144ae8-bd76-45f0-8bc6-c2f932dbfec6)

After logging in using Remote Desktop we can access the ICMPv4 settings throught the Firewall Settings on the VM(Virtual Machine)

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/deb51d93-1df6-4591-9ff7-10a1dd81e110)

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/44a64cfb-6c3a-46ae-bd84-1e7f5031f262)

We can filter the options to sort by ICMPv4 to find the "Rules" we need. After we find the rules under Core Networking Diagnostics they can be enabled.

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/eda6fe6a-8565-431b-ae22-7e327e371c1c)

We can test the connection from Client to DomainC by pinging the DomainC VM from the Client VM, a successfull ping will show theese results.

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/5d1f912a-4ec8-4436-b983-95c0859d6239)

Active Directory can now be installed on the DomainC VM.

Back on the DomainC VM, the Server Manager Page will automatically launch on startup. From here we can click add roles and features.

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/198d3c83-0094-4687-a6f3-d0acf9c9047a)

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/ffada5a3-19cc-4c79-8f78-10d2418ae25f)

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/6b66ab74-9b0b-4808-8860-675ceae3d834)

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/940befe5-d2ec-4098-8d03-9bef15233cc0)

Most of the Settings will be the default until you get to Server Roles, there we can check off the Active Directory Domain Services

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/019e3b55-a3e6-4f1f-95d1-7da064e2dd64)

Continue with the install until complete then close that page.

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/200913ea-c7c7-4be9-aab5-b3fe8f4a5b24)

At the top of the page a flag with a caution sign will appear, there you can promote the VM as a Domain Controller.

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/b88b2c26-2071-41b8-a712-ccbcc0c6833c)

To set up the VM as a Domain Controller we need configure our forest with a unique Domain Name of your choosing (Remember this Domain).

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/eeaba0a4-4902-46ac-bf34-dee4c2020f60)

Moving foward we can create the Directory Services Restore Mode (DSRM) Password.

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/817c076c-ad98-452f-aa9f-0027c22b54c7)

Continue with the Configuration till complete and the VM will need to restart.

<br/> 

After restarting the VM signing in will require the new Domain added into the username of the VM.

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/e6f5b25f-da7d-4f89-9809-100d5a9abeae)

Logging into the now Domain Controller the Server Manager will automatically load, in the Tools menu will be Active Directory Users and Computers(ADUC) page will appear.

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/cc78999d-a622-44f5-9bfd-57a6daf313f0)

Inside ADUC we can make things easier to see by making our own Orginizational Unit to sort Employees and Admins.

<br/>

Right click in the Domain drop down list and add two new Orginizational Units one named :Employees and Admin

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/89988165-de80-4980-a361-f61c4276a06b)

We can now create a Employee who will have admin control in the Domain by right clicking in the admin folder.

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/361c70cb-b2a5-47b1-9efa-83873c9cabe8)

You can name the epmloyee whatever you want just remember the User logon Name.

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/f3283468-1dc2-4127-a91e-b0bd64ee65f0)

In addition to the login name, you will need to make and remember the password you set. (Be sure to uncheck the option to reset password on login)

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/f59ccb44-857f-46dd-a483-7420bb9e4a38)

Continue with the process till the user is finished. The end product will look like this:

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/b8af306b-d6be-4055-8b90-607d1bfb0e0e)

We can now add John Doe to the "Domain Admins" Security Group. We can do this by right clicking on the John Doe profile and click on properties.

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/34d3b493-cd89-4c3a-9fd6-3f2653f121e0)

In the properties menu we can switch to the "Members of" tab and click add.

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/02232b13-6277-4839-ac6e-fefeb2311245)

In the text box we can search for Domain Admins Group then press Check Names and add them to the Domain Admins group.

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/b6b24581-691b-4497-82e7-7b462f516c1c)

Apply the Settings and we have now created an Admin Profile under the name of John Doe. From here on we will be using the John Doe Account as a Admin.

<br/>

We can now connect the Client VM to the Domain by setting the DNS to the DomainC VM's Private IP Address on Azure.

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/513a9ad9-ac7a-44df-a632-c11c4ee7b9d4)

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/ae8d0905-92fe-424e-a774-3eece108c788)

After adding the DNS, restart the VM and login using Remote Desktop as the original user.

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/93cac346-f207-449f-bb48-679b2d13c2a5)

Once inside gp tp the about your PC settings, and scroll down to "Rename this PC Advanced").

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/be5cac51-e400-438c-a5c1-d0af4c130f6f)

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/12c87b0a-1dad-429f-95b6-a78805e90966)

At the bottom of the page we can change the Domain to the one we created by clicking change.

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/63a4496e-65bc-45d0-a5d0-e18b3c049171)

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/070455e4-297c-4aa8-9077-3ec52529e153)

A User and Password will be required to join the domain, use the John Doe Account to login.

<br/>

The Client VM is now connected to the Domain and now we can log in as our Admin John Doe.

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/84d9250c-5569-4632-b307-4e76735cb885)

Once logged in go to the Remote Desktop Settings and select users that can remotely access this PC.

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/a9e54701-e533-4f24-96aa-d0262d13617d)

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/52668e66-5ddd-4f5c-b893-2d7ecc564da1)

We want to add all Domain Users to the list of people that can access Client VM. We will search Domain in the text box and click Domain Users.

![image](https://github.com/Adam-Quevedo/configure-ad/assets/151606017/915bd0f6-b036-4b62-91e4-5fe70bf22c21)


<h1>Congratulations!!!, You have successfullly made set up an Active Directory using Azure</h1>




</p>
