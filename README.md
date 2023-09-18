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
