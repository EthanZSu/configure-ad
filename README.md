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
<img src="https://github.com/user-attachments/assets/a8913aab-9864-41ec-a95b-cb18dec71698" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In the left column right click "mydomain.com".
  <br />
Then select "New".
  <br />
Then select "Organizational Unit".
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/36733108-4daf-4e43-98c7-f745838768fc" height="500%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Name the Organizational Unit: _EMPLOYEES .
  <br />
check the box for Protect container from accidental deletion.
  <br />
Click "OK".
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/b7713872-25aa-4392-95d4-fb5f9d860964" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In the left column right click "mydomain.com".
  <br />
Then select "New".
  <br />
Then select "Organizational Unit".
  <br />
  <br />
Name the Organizational Unit: _ADMINS .
  <br />
check the box for Protect container from accidental deletion.
  <br />
Click "OK".
  <br />
  <br />
Right click & refresh mydomain.com.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/65eb4e9f-ed7b-4a3d-a113-91e08ecd7413" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Right click the: _ADMIN organizational unit,
  <br />
Then select "New".
  <br />
Then select "User".
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/dc38ec0a-2562-4242-b89c-1702fb87aa24" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create a new user inputting the name & user logon name.
  <br />
Then select Next.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/97acf9e9-dc7a-4c05-90c8-2a66a35d6479" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Choose a password.
  <br />
Uncheck: user must change password at next logon.
  <br />
Select password never expires.
  <br />
Select Next, 
  <br />
Select Finish.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/dcbc93b2-a2fe-4357-9c90-7e32f24e5c9e" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click: _ADMINS,
  <br />
Right click: Jane Doe (the admin user account),
  <br />
Then click: Properties.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/cd43abbf-705a-4238-ae46-f35cc3524671" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
At the top select: Member Of,
  <br />
Then click: Add... ,
  <br />
Type: domain,
  <br />
Click: check names.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/66918152-c559-4c11-848c-6044162fb4a0" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Select: Domain Admins,
  <br />
Then select: OK, Apply, OK.
  <br />
  <br />
In the taskbar search: cmd (for command prompt).
  <br />
type: logoff, then hit "ENTER".
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/b27c5a7f-f746-4da1-b124-6ab6bc213c22" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On your actual computer, search for remote desktop from your taskbar search box.
  <br />
Select: Show Options
  <br />
For User name input (whatever your equivalent is to) mydomain.com\jane_admin
  <br />
click Connect.
  <br />
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/a4e208ff-449e-44ee-96c6-ecf2e7cfb73a" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Input the password for the domain account and select ok.
  <br />

</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/115f5e65-dacf-42a6-9284-0a89b038c4a3" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This notification will appear.
  <br />
Select "yes".
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/960c3bef-6829-4b20-a822-47d7345519e4" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
From your taskbar search box, search for cmd (command prompt).
  <br />
In the command prompt type: whoami.
  <br />
Hit ENTER.
  <br />
The result should be: mydomain\jane_admin.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/3bc465f2-854b-47e1-9584-fb4f8e194ffb" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In your Windows computer taskbar search box search: Remote Desktop Connection.
  <br />
In Microsoft Azure search: Virtual Machines & select Client-1 VM.
  <br />
Copy Client-1's Public IP address into the Remote Desktop Connection & Connect.
  <br />
Enter the administrator account credentials for the VM: the "labuser" username & password.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/d2218945-7873-4dfa-8b4d-feaafef2d7b1" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This notification will appear.
  <br />
Select "yes".
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/0d292462-667f-42b9-bd72-4ed831fe0a9a" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On the taskbar right-click the Windows icon.
  <br />
Then select system.
  <br />
Scroll down & select: Rename this PC (advanced).
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/6d870f08-91ea-4619-88cc-21f58b2f4850" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click: Change...
  <br />
Select: Domain.
  <br />
Input: domain.com 
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/6e4ffe79-32bf-4190-8b52-3c3ff402a77e" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Hit ok,
  <br />
You will see the above notification.
  <br />
Hit "ok" again.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/4f23a9a7-8dd9-485c-aecd-873d5124e279" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Back to Microsoft Azure on your computer: search for your DC-1 VM.
  <br />
Copy DC-1's Private IP address.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/d90f9a0b-c98a-40cb-adb9-6768106c2cff" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Microsoft Azure, search for your Client-1 VM.
  <br />
On the left column select Network Settings.
  <br />
click the blue text On the right, below: Network Interface/IP configuration.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/20d9fa13-8fe7-42ca-8046-0d1855a4ed07" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On the left column select DNS Servers.
  <br />
Select custom.
  <br />
Below DNS server paste the DC-1 Private IP address.
  <br />
At the top, select save.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/45cb1f60-a505-4083-9fb0-da3e1ea7a956" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
When Client 1 is done updating, search for Client-1 again.
  <br />
At the top center: click the Restart (which will flush the DNS cache).
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/21ebdb3f-59c4-4e2b-b582-c159aa121d8d" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Login Client-1 with your lab-user account.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/8e18125d-4277-4f8e-b413-e13b0a986509" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
From the taskbar search box, open command prompt.
  <br />
type: ipconfig /all
  <br />
On your keyboard hit ENTER.
  <br />
The DNS server's IP address should be DC-1's private IP address.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/24f175b2-5be3-4f9a-b2c1-38202415b523" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Within the command prompt, ping DC-1's private IP address.
  <br />
You should see 4 replies.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/c427ff42-2a55-43bd-97a8-ee08f582dd0e" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On the taskbar right-click the Windows icon.
  <br />
Then select system.
  <br />
Scroll down & select: Rename this PC (advanced).
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/799d8e47-62b5-40f2-95b6-c1f85f467bb4" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click: Change...
  <br />
Select: Domain.
  <br />
Input: mydomain.com
  <br />
Click OK.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/14efb95a-51ba-4f2a-971f-426b9fe11be9" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Sign in with an account that has permission to join the domain.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/91e83af8-7c08-4084-abf3-12115267a182" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click OK to this notification (which may be behind the other windows).
  <br />
Click OK to the notification prompting you to restart the system.
  <br />
On System Properties, click: Close.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/96556f17-5b2c-4239-84cc-da4d0894fc4b" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On the above pop up click: Restart Now.
  <br />
Click OK to the pop up informing you the Remote Desktop Session has ended.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/7506d841-3e4e-407a-b09e-dced0060cf98" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Login Client-1 with your domain admin account.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/f6d701a2-ba7a-46d3-8823-3db2b82ecca2" height="50%" width="50%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click "yes" to this pop-up.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/fb14f07f-bca1-4cff-8c29-0b9b58ad1225" height="80%" width="80%" alt="Disk Sanitization Steps"</p>
<p>
Close any Microsoft/Windows promotional pop-ups.
  <br />
Right click the Windows start button in the bottom left.
  <br />
Select: System.
  <br />
  <br />
In the right column scroll down & select: Remote desktop.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/cfc908db-ab36-4a0a-8a6a-da5908350f60" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click: Select users that can remotely access this PC.
  <br />
Click: Add.
  <br />
Input: domain users.
  <br />
Click: Check Names.
  <br />
Click: "OK" twice. 
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/37582141-b56e-4d8f-aba8-024891237cc1" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Login DC-1 with your domain admin account.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/830c298b-5e90-4ee9-9810-e3f54c966db1" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click "yes" to this pop-up.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/d13623ec-d17c-46ad-9ab6-fd7a98eefd33" height="95%" width="95%" alt="Disk Sanitization Steps"/>
</p>
<p>
In the Server Manager, select Tools on the right.
  <br />
Open Active Directory Users & Computers.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/df30a343-8f24-4ebc-b09b-24d6af18c71b" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On the left: Select mydomain.com.
  <br />
Then underneath, open the Users folder.
  <br />
Select Domain Users.
  <br />
  <br />
Normally,  multiple users would be added to remote desktop by Group Policy.
  <br />
But for this tutorial, users to access Client-1 will be added a diffrent way.

</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/fdd44339-b1fd-41ef-8770-4eada6bf698b" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Minimize the Server Manager & Active Directory Users and Computers Windows.
  <br />
Close the Domain Users Properties Window.
  <br />
  <br />
In the Windows taskbar search bar, type: Windows Powershell ISE.
  <br />
Right click the "Windows Powershell ISE" & then Run as administrator.
  <br />
Confirm "yes".
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/d1ecca3e-7177-4ce7-9c5d-0df8bed93858" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Powershell ISE, on the left, under File: select the New Script icon.
  <br />
  <br />
Type in the following script 
  <br />
(which will generate 100 random accounts, all using Password1,
  & place all accounts in the EMPLOYEES Organizational unit.)
  <br />
  <br />
Run the script (click the green triangle icon).
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/b8f84a0c-a649-4903-9800-f923d8179fee" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
You may minimize the Powershell ISE window.
  <br />
  <br />
In the taskbar searchbar, search: Administrative Tools.
  <br />
Select: Active Directory Users and Computers.
  <br />
Right click the _EMPLOYEES organizational unit, and refresh.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/47807a28-be3c-4c4c-9036-0d62281829c2" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Select a name, 
  <br />
right click & copy the display name.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/6eb9cdbe-d5d9-4ccb-b07a-c746eeb59596" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Login Client-1 with the previous display name you copied:
  <br />
On Remote Desktop Connection, select show options.
  <br />
Paste the display name after: mydomain.com\
  <br />
Select Connect.
  <br />
Login using Password1
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/23cf43d2-d3dc-479c-9fe2-2630d756007c" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click "Yes" to this pop-up.
  <br />

</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/7d89bf0a-13c4-41ee-8a14-c3dbdb238869" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  Close any Windows promotional pop-ups.
  <br />
  <br />
In the taskbar search bar, search for cmd (command prompt).
  <br />
Type: whoami, click ENTER.
  <br />
You should see the username you logged in with.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/eaf9eb28-f43a-452b-b345-b2909019b125" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Close the Command Prompt.
  <br />
  <br />
Open File Explorer on the taskbar.
  <br />
Select This PC on the left.
  <br />
Select Windows (C:) under Devices and drives.
  <br />
Open the Users folder.
  <br />
You will see a folder for the account you just signed in with.
  <br />
(Every time a new account signs into Client-1, a new folder is made for it.)
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/04e12f62-fbaa-484b-9d6b-4b733130409b" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In DC-1, Close the Properties of the last account name used.
  <br />
  <br />
Pick another account to sign in Client-1 with.
  <br />
As before, copy the display name.

</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/a830c71a-7bb8-4ce8-9025-f00262cdab58" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Login Client-1 with the display name you just copied:
  <br />
On Remote Desktop Connection, select show options.
  <br />
Paste the display name after: mydomain.com\
  <br />
Select Connect.
  <br />
Login the password incorrectly about 10 times
  <br />
(which should lock this account from logging in).
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/531a82ed-51c0-4fd1-bdd6-b40e9c12dd84" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Solution #1: In DC-1 unlock the account that failed to login Client-1:
  <br />
Select the Account Tab.
  <br />
Check the Unlock account box.
  <br />
Then click OK.

</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/02e36090-be2c-4ed4-857e-703628cabd49" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Solution #2: In DC-1 reset the password of the account that failed to login Client-1:
  <br />
Right click the account name.
  <br />
Reset password, then input a new password.
  <br />
Check the Unlock the user's account box.
  <br />
Then click OK.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/1d865000-cb64-4f13-9f31-88ee3f8f7c8a" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To disable an account right click the account name.
  <br />
Then click: Disable Account.
  
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/5ed5dfcd-b141-4ad1-b32c-b11c1a35c52f" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
If the user of the disabled account tried to login into Client-1,
  <br />
he'd see this notification.

</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/d8e49e2c-7f75-4da2-b0ab-a498c59dcae9" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To re-enable the account in DC-1, right click the account name.
  <br />
Then click: Enable account.
  <br />
(Now that account can login to Client-1 again.)
</p>
<br />


<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

  <br />

</p>
<br />


<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

  <br />

</p>
<br />


<p>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

  <br />

</p>
<br />
