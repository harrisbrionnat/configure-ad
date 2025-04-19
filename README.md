<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services


<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Within Azure we will create a Windows 10 and Windows Server 2020 virtual machine
- Enable Active Directory Domain Services on the Windows Server virtual machine
- Join the Windows 10 client machine to the Domain Controller on the Windows Server virtual machine
- Allow non-administrative users to access remote desktop

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  <b> Creating Our Virtual Machines</b> 
First, we will set up a Windows Server 2022 virtual machine which will host our domain controller. Within the Azure portal, go to <b>Virtual Machines</b> --> <b>Create</b>--><b>Axure Virtual Machine</b>
Next, create a new resource group. We will call it 'active-directory-rg'. Our VM name will be active-directory-dc. Region will be West US 2. Image will be Windows Server 2022.Size will be Standard_D2s_v3 - 2 vcpus, 8 GiB memory, Then pick a username and password. Check the licensing agreement. Go to the networking tab. Name the vnet active-directory-vnet. Click Review + Create. Our next virtual machine will be a client machine which will connect to the domain controller on Windows Server. Again select <b>Create</b> on the Virtual Machines tab. Put this vm in the same resource group. Name it 'active-directory-client'. Put it in the same region as our other vm (West US 2) the Image will be Windows 10. The size will be: Standard D2s v3 (2 vcpus, 8 GiB memory). Then pick a username and password. Check the licensing agreement. Got to the networking tab and put this vm in the same vm as the one on Windows Server that we just created. Click Review + Create. 
  <br>
  <br>
  Now we will set the Domain Controller's NIC's Private IP address to static. Go to the Virtual Machines tab, click on active-directory-dc, <b>Networking</b> --> <b>Network Settings</b>. Click on the virtual NIC in the upper middle of the screen. Click <b>ip-config1</b>. Change to private ip setting from dynamic to static
  <br>
  <br>
  For testing purposes, we will disable to Windows Firewall on active-directory-dc. Once logged into the vm. Go to the Windows Firewall by right clicking the start menu and clicking <b>Run</b>. Type wf.msc. Click <b>Windows Defender Firewall Properties</b>. Turn the firewall state to 'off' for the Domain, Private, and Public Profile tabs.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, we will set active-directory-client's dns server to active-directory-dc's private IP address. On active-directory-client, go to <b>Networking</b>--> <b>Network Settings</b>. Click on the virtual nic. Go to <b>DNS Servers</b>. Then choose 'custom' and type in active-directory-dc's private ip. To test, login into active-directory-client and ping active-directory-dc's private ip address. Additionally, you can run ipconfig /all to check if the DNS Settings are the domain controller's private ip.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, we will make active-directory-dc an actual domain controller. Once logged into the vm. We need to install Active Directory Domain Services. On the Server Manager, go to <b>Add Roles and Features</b>. Keep clicking next until you get to <b> Select Server Roles</b>. Check <b>Active Directory Domain Services</b>. Then click 'install'. 
</p>
<br />
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
to promote active-directory-dc to a domain controller, go to the server manager, click on the flag in the upper right hand corner. Click <b>Promote this server to a domain controller</b>. Add a new forest name it: sampledomain.com. Create a password. Click next through the prompts and install. The computer should automatically restart.
</p>
<br />
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now, create a domain admin user within the domain controller with the newly created domain user credentials. It should looking like: DOMAIN\user and then your password. We will not create a domain admin account. Go to <b>Active Directory Users and Computers</b>. Right click <b>mydomain.com</b> and add two <b>Organizational Units</b> one will be _EMPLOYEES and the other will be _ADMINS. Create a user to put in the _ADMINS organizational unit. Right-click the OU and click <b>add</b> --><b>organizational unit</b>. Add the users first and last name along with the domain account name. We can add this user to the Domain Admins Security group by right clicking <b>Properties</b>--><b>Member of</b>--> <b>Add</b>. In the box, type 'Domain Admins' and click 'apply' and 'ok'. Now logout and log in as the domain admin.
</p>
<br />
