<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### (https://www.loom.com/share/edb290e0da8e45ca9a07a51403e29d92?sid=5b79770c-4ad5-4da3-a370-11f63c7def4b)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computer)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Domain Controller (DC)
- Static IP Address for DC
- Acive Directory
- Join Clients to Domain

<h2>Deployment and Configuration Steps</h2>

<p>
1. Go to portal.azure.com and create a resouce group. Alternatively, you could just create a virtual machine and let it automatically create a resource group for you. We will need to ensure that both VMs we create are in the same resource group and on the same Vnet. 

2. Create a the Domain Controller VM. Make sure it is placed into the resource group that we created. Name the virtual machine "DC-1". For the image, you need to use Windows Server 2022. Allow it to create a Vnet for us and take not of the Vnet that gets created. We will need it in the next step. Click Review and Create.

<img width="688" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/250fb561-94d0-44ee-aeb0-7358926d87cf">
<img width="777" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/062aa536-b43e-4ade-a2da-74753d709825">

3. Create the Client virtual machine. Click vvitual machine -> Create New. Name this virtual machine "Client-1". Place it in the same resource group and Vnet that we created prior. For the image on this virtual machine, we will use Windows 10. Click until we get to networking and make sure the client is on the same Vnet as the previous virtual machine. If it is not showing up for some reason, refresh and then create the machine again. This is an important step as DC-1 and Client-1 need to be on the same V-Net.

<img width="685" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/132203b5-cefb-4754-9ec5-a47bbece5fd0">

4. Set the Domain Controllers NIC Private IP address to be static. We do this step because we don't want the DC's ip address changing. we want it to stay the same. To do that, in the azure portal, click the DC virtual machine -> Networking -> Click the link to the right of the words "network interface" -> ip configuration in the left panel -> ipconfig -> Click static and save the changes

<img width="492" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/057ddcd3-17b8-4987-9d09-312b5d09c652">
<img width="245" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/e7178c63-2ebd-487f-a784-e3efb98b08dd">
<img width="519" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/4d272543-a896-4eff-b4e4-a9a29270a352">

If you want to ensure that both Virtual Machines are on the same Vnet, in the search type Network Watcher -> Monitoring -> Topology. Note how you can see that both of my VMs are on the same Vnet.

<img width="948" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/c09aa6df-974f-4c5e-ac40-c958a69d2fee">

5. To ensure that connectivity between the client and domain controller, log into client- 1 on the microsoft remote desktop and ping DC-1's private IP with a perpetual ping (-t). It should fail. While the ping is still going, log into DC-1 type firewall in the start menu -> click advanced firewall settings -> enable ICMPv4 on the firewall -> note how the traffic is allowed now back in client-1. To stop the ping, cmd (control)-C. Connectivity has been verified.

<img width="977" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/126b13fb-8f23-4f32-bd16-a746aa8e78ea">
<img width="690" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/1c969b31-fb20-4006-bea5-ed5582cf9da5">
<img width="201" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/85036ae6-c107-4c66-9a5a-24e98d475bd9">
<img width="1029" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/3623baea-81f6-47d3-806e-fc7240412cfa">
<img width="975" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/50176bfb-9015-49be-a651-96e943d80b82">

6. Install Active Directory. Add roles and features -> Active Directory Domain Services -> Install -> Close. Promote as a DC by clicking the yellow triangle at the top right -> click "promote this domain to a domain controller" -> setup new forest -> create a root domain name (i just used ministryofmagic.com) -> install. Restart and log back into DC-1 as user ministryofmagic.com\jfields (or whatever you named yours) 

<img width="784" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/7daf0431-4980-4436-bc2a-ea957fb43cbe">
<img width="285" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/5eb9e6ab-f3e5-4e44-b730-56a4e31a221e">
<img width="1245" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/ce26ad97-0a5f-456f-8f11-50864b74975e">

7. Create 3 Organizational Units in the servar manager by clicking tools in the right corner -> Active Directory Users and Computers -> Right Click -> New -> Organizational Unit (OU) -> Create a new unit named _EMPLOYEESS and then use the same process to create OUs _ADMINS and _CLIENTS. Finally, create a new user named "Harry Potter" (right click-> new-> user) with a user name "harry_admin". Add Harry to the "Domain Admins" security group by double clicking -> member of -> add -> type "domain" -> check names -> domain admins -> apply and okay. 

<img width="1044" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/d63168f6-7618-4193-9ebb-cb24e2fb27a4">
<img width="746" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/ee5e951b-b0e1-4401-8199-2c55d3f11577">
<img width="499" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/fe49a417-1f1f-488d-82a4-f83269fe232b">

8. In the Azure portal, join Client-1. To do that, we need to set Client-1's DNS settings to DC's private ip address. First retrieve DC's ip address, then go into client-1's virtual machine -> Networking  -> Network interface -> DNS servers -> Custom -> enter DC's private IP address -> save. Restart the virtual machine in the azure portal. Now, log back into the original admin (mine was jfields) and join it to the domain (if you skip this step, you will get an error). Do this by start -> settings -> system -> About -> Rename this PC advanced -> click domain and enter the domain that you created then enter the credentials. It should welcome you if you did it correctly and restart. Login to the domain controller  and verify client-1 shows up in Active Directory Users and Computers

<img width="1034" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/fa5e2f92-68a9-4682-8cc7-17cb58ec4c20">
<img width="947" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/44ca6173-1266-45cf-90f9-ee80c1363c25">
<img width="370" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/979a03ab-e93f-4f50-b2d9-2590da9e5349">
<img width="324" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/01c3e318-2d37-4654-b3c7-ece96830b53c">
<img width="735" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/aaad353b-0931-41b1-b189-edd0bcb48058">

9. Setup Remote Desktop for non-administative users. Log on to Client-1 as the domain you created -> start -> settings -> System -> and Remote Desktop. Then click select users that can remotely access this PC -> add -> type domain users and check names -> press "okay" 

<img width="902" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/018089ba-4061-40d4-93c6-1cc50fbb6a3c">
<img width="376" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/ee9fa6c1-8099-458f-bfb4-8cabf3528cc6">

10. Create a bunch of additional users and attempt to log in with one at the end. Open Powershell ISE as an administrator (right click and run as administrator). Create a new file and paste the contents of the script from here (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1). Run the script and observe the accounts being created into the _EMPLOYEES folder that you created. Log in to one of the user names in Client-1 Note: If you keep getting red notifications while trying to the running the script, it is more the likely possible that you didn't run the Powershell ISE as an admin. Just close it and start over

11. Congratulations. You now have Active Directory installed on your virtual machine

<img width="720" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/4b725697-876d-4b6a-9a13-7447b364b660">
<img width="745" alt="image" src="https://github.com/JavariusFields/configure-ad/assets/144845191/f25baa4d-6b0e-4b9c-ad65-32628b52eccf">












