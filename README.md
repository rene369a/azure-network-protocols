<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups using a Mac OS. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04
- Mac Os (user)

<h2>High-Level Steps</h2>

- Create Resource Group with 2 Virtual Machines, Windows 10 VM, Linux (Ubuntu) VM, on the same Virtual Network (Vnet) and Subnet
- Connect to Windows VM using remote desktop (download Microsoft Remote Desktop on Mac) and dowload/install Wireshark
- Open Wireshark, filter for ICMP traffic only, retreive Linux VM private IP and ping from Windows VM and observe ping requests
- Open Network Security Group for Ubuntu VM and disable incoming (inbound) ICMP traffic, observe ICMP traffic, Re-enable ICMP traffic for NSG your Ubuntu VM is using
- Filter and observe each, SSH Traffic, DHCP Traffic, DNS Traffic, RDP Traffic

<h2>Actions and Observations</h2>

<p>
<img width="1670" alt="Screenshot 2023-08-17 at 6 05 00 PM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/10b20718-1302-4003-8087-f572ff74480a">
</p>
<p>
- First, create one Resource Group for both Virtual Machines and take note of the region, as both VM's will use the same one.
</p>
<br />

<p>
<img width="1670" alt="Screenshot 2023-08-17 at 6 12 50 PM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/7da823ed-7626-47b8-a855-5e77432156c8">
</p>
<p>
- Search for Virtual Machines and let' start by creating our first VM, a Windows 10 VM and name it VM1. Create a username and password, which we will need to RDP into our VM.
</p>
<p>
  <img width="1670" alt="Screenshot 2023-08-17 at 6 16 03 PM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/77bf8177-8b2d-4b79-9630-e78f1d8d0dce">
<img width="1670" alt="Screenshot 2023-08-17 at 6 17 21 PM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/002c0412-b493-49d3-a4fb-ce6a5c249254">
</p>
<p>
- Make sure you check the licensing box before continuing and the standard 2vCPUs is plenty for this exercise.
<br />

<p>
<img width="1670" alt="Screenshot 2023-08-17 at 6 22 41 PM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/9874c653-2bdf-4c64-98b0-47cea9e76fef">
</p>
<p>
- On the Networking tab, take note of your Virtual Network (Vnet) as both VM's will be on the same Vnet. Select review+create and then, create after validation passed. VM1 is almost ready.
</p>
<p>
  <img width="1670" alt="Screenshot 2023-08-17 at 6 30 50 PM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/a28a6af2-026c-4507-8328-ca8523cfe917">
</p>
<br />

<p>
- While VM1 is finishing, we can create our second VM running Linux (Ubuntu), instead of Window, in the same Resource group and region. Name it VM2
</p>
<p>
  <img width="1670" alt="Screenshot 2023-08-17 at 6 37 41 PM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/f563db3a-de91-4670-b5b4-26337adfb30a">
  <img width="1670" alt="Screenshot 2023-08-17 at 6 38 44 PM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/6817c3ad-27e8-410e-8bc7-ac236bee4b6b">
</p>
<p>
- Make sure to change from SSH public Key to password and create a username and password.
</p>
<br />


<p>
<img width="1670" alt="Screenshot 2023-08-17 at 6 50 21 PM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/65c79e16-b562-4d9a-aced-46e007fd113a">
</p>
<p>
- Double check that VM2 had the same Virtual Network as VM1, it should, and the subnet automatically applys. Click on review+create and create after validation. Your second VM running Linux is ready.
</p>
<br />

<p>
<img width="1670" alt="Screenshot 2023-08-17 at 6 05 00 PM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/10b20718-1302-4003-8087-f572ff74480a">
</p>
<p>
- First, create one Resource Group for both Virtual Machines and take note of the region, as both VM's will use the same one.
</p>
<br />
