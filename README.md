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
- Double check that VM2 has the same Virtual Network as VM1, it should, and the subnet automatically applys. Click on review+create and create after validation. Your second VM running Linux is ready.
</p>
<br />

<p>
<img width="1670" alt="Screenshot 2023-08-18 at 9 45 00 AM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/e79e9ffc-4022-4e46-9e50-4b8ba61f64af">
</p>
<p>
- You should now have 2 VM's ready to connect to each other on our Vnet. First, we must RDP into our Windows 10 VM using the public IP address, which we can locate after clicking on VM1. For Mac OS, dowloand and istall Microsoft Remote Desktop as it's needed in order to RDP into our Windows VM. Next, we will open Remote Desktop, copy and paste VM1's public IP address, add and connect to VM1 using our username and password from before. Click on continue for the certification.
</p>
<p>
  <img width="1670" alt="Screenshot 2023-08-18 at 9 52 50 AM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/099ea4a2-c178-4a53-99f2-d1ac41739d1f">
  <img width="1670" alt="Screenshot 2023-08-18 at 9 59 53 AM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/8fdc4826-f9a4-4714-965d-b1dbe45eb3d2">
</p>
<br />

<p>
<img width="1670" alt="Screenshot 2023-08-18 at 10 07 41 AM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/0fe1481b-cbc9-4911-b559-b896e3c82a62">
</p>
<p>
- It will connect to your Windows 10 VM and we can continue after it is done loading. Allow VM1 to access other pc's on the network when prompted and open up the web browser, head to google.com where you will search for Wireshark and dowload/install the program to VM1.
</p>
<br />

<p>
<img width="1670" alt="Screenshot 2023-08-18 at 10 18 04 AM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/078bf511-31c6-4524-90ca-fc993395e217">
</p>
<p>
- After installation we can proceed with opening Wireshark and click on Ethernet to start capturing packets. 
</p>
<p>
  <img width="1670" alt="Screenshot 2023-08-18 at 10 19 30 AM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/1897b5eb-fbf3-45a1-af88-0158cf58d90a">
  </p>
<p>
- Next, we will filter for ICMP and try to ping VM2 from VM1 using the private network IP address for VM2. Open Command Promt on VM1 and "ping (private IP address)" and observe network activity through Wireshark.
  </p>
<p>
<img width="1670" alt="Screenshot 2023-08-18 at 10 21 27 AM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/f15e84fd-545a-4e38-94e9-0041884d842c">
</p>
<br />

<p>
<img width="1670" alt="Screenshot 2023-08-18 at 10 39 23 AM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/fea48bc8-264a-4df5-9d13-e083c7656972">
  <p>
- In this next step, we will do a perpetual ping from VM1 to VM2 and disable incoming ICMP traffic using our Network Security Group (NSG)
</p>
<img width="1670" alt="Screenshot 2023-08-18 at 10 39 38 AM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/840a9e2f-9fb5-49b8-9d49-874fd8b49657">
</p>

<p>
  <img width="1670" alt="Screenshot 2023-08-18 at 10 36 42 AM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/fc578903-a341-4e3f-8f07-d93b69d15340">
  <img width="1670" alt="Screenshot 2023-08-18 at 10 37 37 AM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/564ed199-a3ce-4f7c-88b9-98acf98623dd">
</p>
<br />

<p>
<img width="1670" alt="Screenshot 2023-08-17 at 6 05 00 PM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/10b20718-1302-4003-8087-f572ff74480a">
</p>
<p>
- First, create one Resource Group for both Virtual Machines and take note of the region, as both VM's will use the same one.
</p>
<br />

<p>
<img width="1670" alt="Screenshot 2023-08-17 at 6 05 00 PM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/10b20718-1302-4003-8087-f572ff74480a">
</p>
<p>
- First, create one Resource Group for both Virtual Machines and take note of the region, as both VM's will use the same one.
</p>
<br />
<p>
<img width="1670" alt="Screenshot 2023-08-17 at 6 05 00 PM" src="https://github.com/rene369a/azure-network-protocols/assets/142533276/10b20718-1302-4003-8087-f572ff74480a">
</p>
<p>
- First, create one Resource Group for both Virtual Machines and take note of the region, as both VM's will use the same one.
</p>
<br />
