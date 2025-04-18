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
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
