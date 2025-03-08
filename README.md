<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


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

<h2>High-Level Steps</h2>

- Create Resource Group
- Create Windows 10 Virtual Machine (VM)
- Create a  Linux (Ubuntu) VM
- Ensure Both VMs are in the same Network/ Subnet

<h2>Actions and Observations</h2>

<p>
<img style="display: block;-webkit-user-select: none;margin: auto;cursor: zoom-in;background-color: hsl(0, 0%, 90%);transition: background-color 300ms;" src="https://github-production-user-asset-6210df.s3.amazonaws.com/142127371/420568330-5fbaaefd-7cd7-4c41-809d-0a0c0d4e2a5e.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&amp;X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20250308%2Fus-east-1%2Fs3%2Faws4_request&amp;X-Amz-Date=20250308T064313Z&amp;X-Amz-Expires=300&amp;X-Amz-Signature=34498fd4afc4e4d4aba8b58d2d1536feee8fd41b52709fe5c8b508196d4c9613&amp;X-Amz-SignedHeaders=host">
</p>
<p>
Create a Resource Group
Create a Windows 10 Virtual Machine (VM)
While creating the VM, select the previously created Resource Group
While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet
Create a Linux (Ubuntu) VM
While creating the VM, select the previously created Resource Group and Virtual Network—the Virtual Network MUST BE THE SAME.
Authentication type: Username/Password
Ensure both VMs are in the same Virtual Network / Subnet

</p>
<br />

<p>
<img style="display: block;-webkit-user-select: none;margin: auto;cursor: zoom-in;background-color: hsl(0, 0%, 90%);transition: background-color 300ms;" src="https://github-production-user-asset-6210df.s3.amazonaws.com/142127371/420562561-d22d0f1f-a23d-4e8c-baf5-7a91f0709866.PNG?X-Amz-Algorithm=AWS4-HMAC-SHA256&amp;X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20250308%2Fus-east-1%2Fs3%2Faws4_request&amp;X-Amz-Date=20250308T063035Z&amp;X-Amz-Expires=300&amp;X-Amz-Signature=c3c9712a2c55f0ef7ce44e3d47c4a14ed439b79c5026810ab6ff7e8019186626&amp;X-Amz-SignedHeaders=host">
</p>
<p>
If using Mac, install Microsoft Remote Desktop
Use Remote Desktop to connect to your Windows 10 Virtual Machine
Within your Windows 10 Virtual Machine, Install Wireshark
Open Wireshark and start packet capture
Within Wireshark, filter for ICMP traffic only
Retrieve the private IP address of the Ubuntu VM (linux-vm) and attempt to ping it from within the Windows 10 VM
Observe ping requests and replies within WireShark
From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark

</p>
<br />

<p>
<img style="display: block;-webkit-user-select: none;margin: auto;cursor: zoom-in;background-color: hsl(0, 0%, 90%);transition: background-color 300ms;" src="https://github-production-user-asset-6210df.s3.amazonaws.com/142127371/420567914-94d3ab71-0ad8-4482-a726-6a0ac9ccecb0.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&amp;X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20250308%2Fus-east-1%2Fs3%2Faws4_request&amp;X-Amz-Date=20250308T063831Z&amp;X-Amz-Expires=300&amp;X-Amz-Signature=92bc63faa24e0527d6c52d972a26ed737071e8b25e2f1c3de2d4d4536c0d3c7c&amp;X-Amz-SignedHeaders=host">
</p>
<p>
(Configuring a Firewall [Network Security Group])
Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM
Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic
Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity
Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is
Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)
Stop the ping activity

</p>
<br />

<p>
<img style="display: block;-webkit-user-select: none;margin: auto;cursor: zoom-in;background-color: hsl(0, 0%, 90%);transition: background-color 300ms;" src="https://private-user-images.githubusercontent.com/142127371/420566361-01f3faca-fc0e-4efa-acc9-62039c65ccd0.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NDE0MTU5NTAsIm5iZiI6MTc0MTQxNTY1MCwicGF0aCI6Ii8xNDIxMjczNzEvNDIwNTY2MzYxLTAxZjNmYWNhLWZjMGUtNGVmYS1hY2M5LTYyMDM5YzY1Y2NkMC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwMzA4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDMwOFQwNjM0MTBaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0wMzRlMmM2YzVhMDY1Zjc5ZTljZTBiZWM4MmM2OGQxNDFkZDQ5NDFhMDZhZDBhOGIxYTk3Mjg5OGQ3OTQ4MWEzJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.bFCFwQjGmmSt80wfrrazom0Ui6MlQ_219i7F-cEO3M8">
</p>
<p>
(Observe SSH Traffic)
Log back into the windows-vm
Back in Wireshark, start a packet capture up
Filter for SSH traffic only
From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)![Uploading Screenshot (132).png…]()

Open PowerShell, and type: ssh labuser@<private IP address>
Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark
Exit the SSH connection by typing ‘exit’ and pressing [Enter]
</p>
<br />

<p>
![Image](https://github.com/user-attachments/assets/8000443e-0ee6-4ef5-a963-c3acd413d232)</p>
<p>
(Observe DHCP Traffic)
Back in Wireshark, filter for DHCP traffic only
From your Windows 10 VM, attempt to issue your VM a new IP address from the command line
Open PowerShell as admin and run: ipconfig /renew
Observe the DHCP traffic appearing in WireShark
</p>
<br />

<p>
<img style="display: block;-webkit-user-select: none;margin: auto;cursor: zoom-in;background-color: hsl(0, 0%, 90%);transition: background-color 300ms;" src="https://github-production-user-asset-6210df.s3.amazonaws.com/142127371/420630659-3f7674fd-3689-47e1-b4c0-9b1923dacaa1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&amp;X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20250308%2Fus-east-1%2Fs3%2Faws4_request&amp;X-Amz-Date=20250308T233454Z&amp;X-Amz-Expires=300&amp;X-Amz-Signature=e0a1ac4a3778bf34bda546859bdf6657dd13b7adff7828e1ba2202eeb0a87dfc&amp;X-Amz-SignedHeaders=host")

</p>
<p>
(Observe DNS Traffic)
Back in Wireshark, filter for DNS traffic only
From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are
Observe the DNS traffic being show in WireShark
</p>
<br />

<p>
<img style="display: block;-webkit-user-select: none;margin: auto;cursor: zoom-in;background-color: hsl(0, 0%, 90%);transition: background-color 300ms;" src="https://github-production-user-asset-6210df.s3.amazonaws.com/142127371/420567017-21f7e80d-864f-4a91-923f-20a59b444b51.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&amp;X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20250308%2Fus-east-1%2Fs3%2Faws4_request&amp;X-Amz-Date=20250308T062507Z&amp;X-Amz-Expires=300&amp;X-Amz-Signature=63d974eca2c848622f314c3bc8aaef8ea7704ab9996f202b9f6b5e79284408d1&amp;X-Amz-SignedHeaders=host">
</p>
<p>
(Observe RDP Traffic)
Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)
Observe the immediate non-stop spam of traffic? Why do you think it’s non-stop spamming vs only showing traffic when you do an activity?
Answer: because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted
</p>
<br />

