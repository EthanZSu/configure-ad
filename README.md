# configure-ad
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
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://github.com/EthanZSu/configure-ad/assets/168872181/c504a3f7-7f55-43c4-b8af-d9cebcfe8304" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
First, a new resource group must be made where the virtual machines will be placed  in.
  <br />
In the top search bar search: resource group and then in top left click "create".
  <br />
  <br />
Name the new resource group.
  <br />
Also select which subscription account to place the resource group under.
  <br />
And pick which geographic region you want the resource group in.
  <br />
  <br />
Then create the resource group.
</p>
<br />



<p>
<img src="https://github.com/EthanZSu/configure-ad/assets/168872181/31f7cd88-e7f3-41d1-ad16-082c3298cdcf" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In the top search bar search: virtual machines, then click "create", then "Azure Virtual Machine".
  <br />
  <br />
For the 1st virtual machine: Select a subsciption account, the resource group just made, & the geographic region you want the VM in.
  <br />
Name this 1st VM something like "domain controller" (because it will have the domain controller with the active directory).
  <br />
The above redundancy & security settings will suffice.
  <br />
The image (VM's operating system) will be Windows Server 2022 Datacenter.
  <br />
VM architecture x64 will suffice.
</p>
<br />



<p>
<img src="https://github.com/EthanZSu/configure-ad/assets/168872181/7a866bf3-00e8-486d-b7a8-17874c1ea230" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Select size "2 vcpus" (2 virtual CPU's).
  <br />
Set up administrator account info for the VM: the username & password.
  <br />
Public inbound ports must allow selected ports, and allow RDP 3389 (for remote desktop to the VM).
  <br />
Scroll down & confirm you want to use an existing windows server license.
  <br />
Also confirm you have the eligible Windows server license.
  <br/ >
  <br />
Create the VM.
</p>
<br />



<p>
<img src="https://github.com/EthanZSu/configure-ad/assets/168872181/28e6888c-1ded-4436-84f9-e962f3c2ebb5" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
You must wait ~5 minutes before making the 2nd VM (so the 2nd VM can be placed in the same network as the 1st).
  <br />
In the top search bar search: virtual machines, then in top left click "create", then "Azure Virtual Machine".
  <br />
  <br />
For this 2nd virtual machine: the subsciption account, resource group, & the geographic region should match the 1st VM's.
  <br />
Name this 2nd VM (maybe something like "Client-1").
  <br />
The above redundancy & security settings will suffice.
  <br />
The image (VM's operating system) will be Windows 10 Pro. Vers. 22H2
  <br />
VM architecture x64 will suffice.
</p>
<br />



<p>
<img src="https://github.com/EthanZSu/configure-ad/assets/168872181/d06279b1-c84a-406f-845d-69e430089eff" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Select size "2 vcpus" (2 virtual CPU's).
  <br />
Set up administrator account info for the VM: the username & password.
  <br />
Public inbound ports must allow selected ports, and allow RDP 3389 (for remote desktop to the VM).
  <br />
Confirm you have the eligible Windows 10/11 license.
</p>
<br />



<p>
<img src="https://github.com/EthanZSu/configure-ad/assets/168872181/a7c686ac-a25e-4bb9-bae1-d6a8add08603" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
At the bottom click Next:Disks, then click Next:Networking.
  <br />
  <br />
For the 2nd VM, the virtual network must match the 1st VM's.
  <br />
The subnet, & public IP will be automatically made.
  <br />
For the NIC network security group select "basic".
  <br />
Public inbound ports must allow selected ports, and allow RDP 3389 (for remote desktop to the VM).
  <br />
Scrolling down, enable accelerated networking & select no load balancing.
  <br />
  <br />
Finally, Create this 2nd VM.
  <br />
Note that Azure may take 5 minutes to deploy the VM.
</p>
  <br />



<p>
<img src="https://github.com/EthanZSu/configure-ad/assets/168872181/95c1d4d7-fee9-4c77-a551-26279e46e989" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Search for your DC-1 (domain controller) VM.
  <br />
select it, & on the left menu scroll down & select network settings.
  <br />
select the blue: dc-#### (primary)/ipconfig1 (primary).

</p>
<br />



<p>
<img src="https://github.com/EthanZSu/configure-ad/assets/168872181/c0d5058d-14fb-49bb-aaba-8aeb59db3fe6" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click the blue ipconfig1.
  <br />
On the right menu, set allocation to static (so DC-1's IP address doesn't change & other computers won't try retrieving the IP address from the DHCP server).
  <br />
  <br />
On the bottom, save.
</p>
<br />



<p>
<img src="https://github.com/EthanZSu/configure-ad/assets/168872181/bc95f65d-38ad-477d-902c-7c1d85f45b4a" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In your Windows computer taskbar search box search: Remote Desktop Connection.
  <br />
In Microsoft Azure search: Virtual Machines & select Client-1 VM.
  <br />
Copy Client-1's Public IP address into the Remote Desktop Connection & Connect.
  <br />
Enter the administrator account credentials for the VM: the username & password.
</p>
<br />


<p>
<img src="https://github.com/EthanZSu/configure-ad/assets/168872181/3e235922-2d99-4a74-91eb-5214b636a28e" height="60%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This notification will appear.
  <br />
Select "yes".  
</p>
<br />



<p>
<img src="https://github.com/EthanZSu/configure-ad/assets/168872181/b41ed23c-61e8-4e71-b4e7-cabc3273cee6" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Select "No" to all the privacy settings (as none of those features will be needed).
<br />
Then accept.
<br />
On the right click "yes" to the network pop-up "do you want... your PC to be discoverable by other... devices on this network?"
</p>
<br />



<p>
<img src="https://github.com/EthanZSu/configure-ad/assets/168872181/222b2fed-54c7-425b-ba6e-4b84ab8ad99e" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
If there is any Windows promotional pop-up, exit it.
  <br />
  <br />
In the taskbar searchbox: search for cmd (command prompt).
  <br />
In Microsoft Azure: Copy DC-1's private IP address &
  <br />
Initiate a non-stop ping from your Client-1 VM command prompt to your DC-1 VM.
  <br />
You will see the ping fail.


</p>
<br />



<p>
<img src="https://github.com/EthanZSu/configure-ad/assets/168872181/644b7db1-3bb8-4d31-8974-80eddb7cfd36" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In your Windows computer taskbar search box search: Remote Desktop Connection.
  <br />
In Microsoft Azure search: Virtual Machines & select DC-1 VM.
  <br />
Copy DC-1's Public IP address into the Remote Desktop Connection & Connect.
  <br />
Enter the administrator account credentials for the VM: the username & password.
</p>
</p>
<br />



<p>
<img src="https://github.com/EthanZSu/configure-ad/assets/168872181/b350477a-7657-442f-ac1f-19f7a3a5ad1f" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This notification will appear.
  <br />
Select "yes".
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/9961efa9-504c-4677-b845-0f560db9246e" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In your Windows computer taskbar search box search: Windows Defender Firewall With Advanced Security.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/9c73d3d3-cfae-4f7d-96f0-07a26ae631d0" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Maximize the window.
  <br />
In the left column, select Inbound Rules.
  <br />
Expand the Name column.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/05b543f7-8045-4dac-bf82-420ac7c7f0c0" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
You can compress the Actions menu on the right.
  <br />
Select both Protocols: ICMPv4, with the Name: Core Networking Diagnostics - ICMP Echo Request (ICMPv4-In).
  <br />
Right click both ICMPv4 Protocols, Enable Rule.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/88162fa8-d0c0-4940-af65-f9f733a905c7" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On Client-1's command prompt, you will see the replies from DC-1. 
  <br />
On your keyboard stop the ping by clicking: CTRL + C.
  <br />
Close the command prompt. 
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/386c07bd-cbf6-49ae-88de-1d2df5d36b52" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Back to DC-1, you may minimize DC-1's: Windows Defender Firewall With Advanced Security.
  <br />
Select the Windows Start icon on the taskbar.
  <br />
Select Server Manager.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/e095b2c0-63ec-4913-950f-f9f8fe6a94a8" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Select: 2 Add roles and features,
  <br />
Click "Next" until you reach the list of Roles.
  <br />
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/69379890-1ed4-45d3-b57f-e7fa3f6dd3b0" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click the box for: Active Directory Domain Services.
  <br />
Add Features.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/328ab95e-ba69-4ada-9de1-ef13507a0bb1" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click "Next" until you can install, and then select the "Install". 
  <br />
When the installation is complete, close the: Add Roles and Features Wizard.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/30162b9e-00c7-4329-88a2-7f2b1f320c02" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On the top right, click the flag icon left of "manage".
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/e764c936-280b-4908-bf90-71f4e507a58a" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click: Promote this server to a domain controller.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/03b9b893-587a-4de2-9415-2b13c769f527" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Select: Add a new forest.
  <br />
Name the Root domain name (maybe something like "mydomain.com").
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/bb96b20e-0574-499b-be27-79f92ce79903" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Select Next, 
  <br />
Assign a DSRM password.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/2c4338ad-d9bc-4556-a9c9-e376c9fa5442" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Select Next,
  <br />
Uncheck "DNS Delegation",
  <br />
Keep clicking "Next" until you can install, and then install. 
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/90928aeb-4ca5-496b-994b-c900131d2973" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Note: You may be signed out of the virtual machine if it automatically restarts.
</p>
<br />




<p>
<img src="https://github.com/user-attachments/assets/28f9a6f5-14f5-4813-a41e-54831b973a60" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Microsoft Azure search: Virtual Machines & select DC-1 VM.
  <br />
Copy DC-1's Public IP address into the Remote Desktop Connection & Connect.
  <br />
Enter the administrator account credentials for the VM: the username & password.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/e132f06a-e571-43e6-9f7f-08fab33f0a55" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This notification will appear.
  <br />
Select "yes".
  <br />
Note that loading may take a while.
  <br />
  <br />
Exit the "Try Windows Admin Center and Azure Arc today" notification.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/e0565b02-a090-48c9-bfe8-30edcd39cd7c" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In the Server Manager Window's top right: select Tools,
  <br />
Then select Active Directory Users and Computers.
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
