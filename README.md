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
First, create one Resource Group for both Virtual Machines and take note of the region, as both VM's will use the same one.
</p>
<br />

<p>
<img width="1670" alt="Screenshot 2023-08-17 at 6 12 50 PM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/7da823ed-7626-47b8-a855-5e77432156c8">
</p>
<p>
Search for Virtual Machines and let' start by creating our first VM, a Windows 10 VM and name it VM1.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
