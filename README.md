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
<img width="1920" height="1080" alt="Screenshot (126)" src="https://github.com/user-attachments/assets/413ca883-415a-45bd-977d-aaa3c1dd8d8d" />
<img width="1920" height="1080" alt="Screenshot (128)" src="https://github.com/user-attachments/assets/d9203ee8-02d8-4d64-bbce-40b615933fee" />
<p>
Create a Resource Group and create a Windows 10 Virtual Machine (VM)
Then select the previously created Resource Group, and allow it to create a new Virtual Network (Vnet) and Subnet
</p>
<br />
  
<img width="1920" height="1080" alt="Screenshot (130)" src="https://github.com/user-attachments/assets/f067e7ec-935b-425e-a7dc-35cf07b5388e" />
</p>
<p>
Create a Linux (Ubuntu) VM as well.
Select the previously created Resource Group and Virtual Network.
  The Virtual Network MUST BE THE SAME.

</p>
<br />

<p>
<img width="1903" height="963" alt="WireShark installation page" src="https://github.com/user-attachments/assets/a3a3d828-05dc-4251-95b4-5c46ae7616bc" />

</p>
<p>
Within your Windows 10 Virtual Machine, Install Wireshark (www.wireshark.org/download.html)
Open Wireshark and start packet capture
Within Wireshark, filter for ICMP traffic only
Retrieve the private IP address of the Ubuntu VM (linux-vm) and attempt to ping it from within the Windows 10 VM
Observe ping requests and replies within WireShark
From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark

</p>
<br />
<img width="1920" height="1080" alt="Screenshot (134)" src="https://github.com/user-attachments/assets/dd589afe-8ae1-4ea7-a7c2-7ffb875a25ce" />

<p>
Open Wireshark and start packet capture
Within Wireshark, filter for ICMP traffic only
Retrieve the private IP address of the Ubuntu VM (linux-vm) and attempt to ping it from within the Windows 10 VM
Observe ping requests and replies within WireShark
From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark

</p>
<br />

<p>
<img width="1920" height="1080" alt="Screenshot (133)" src="https://github.com/user-attachments/assets/b35353b0-6d31-4ad1-aa2a-b5e5672772db" />
</p>
<p>
(Configuring a Firewall [Network Security Group])
Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM
Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic
Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity
<img width="1920" height="1080" alt="Screenshot (134)" src="https://github.com/user-attachments/assets/faeb7876-e99c-4f62-8eae-2640544cfe40" />

Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is
Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)
Stop the ping activity

</p>
<br />

<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e2c48ba1-8d23-4c4a-af42-5ae24b17a144" />

</p>
<p>
(Observe SSH Traffic)
Log back into the Windows-VM
Back in Wireshark, start a packet capture up From Your Windows 10 “SSH into” your Ubuntu Virtual Machine (via its private IP address)! Open PoweShell, and type: ssh labuser@ Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark Exit the SSH connection by typing ‘exit’ and pressing [Enter]"
Open PowerShell, and type: ssh labuser@<private IP address>
Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark
Exit the SSH connection by typing ‘exit’ and pressing [Enter]
</p>
<br />

<p>
<img width="1920" height="1080" alt="Screenshot (155)" src="https://github.com/user-attachments/assets/a4877570-e7c8-4f7f-9098-fee49216d96e" />

<p>
(Observe DHCP Traffic)
Back in Wireshark, filter for DHCP traffic only
From your Windows 10 VM, attempt to issue your VM a new IP address from the command line
Open PowerShell as admin and run: ipconfig /renew
Observe the DHCP traffic appearing in WireShark
</p>
<br />

<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2794944b-fb1a-446e-9e5b-f92ce35e5534" />


</p>
<p>
(Observe DNS Traffic)
Back in Wireshark, filter for DNS traffic only
From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are
Observe the DNS traffic being show in WireShark
</p>
<br />

<p>
<img <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ffb52946-6327-4cca-9db3-dd35b1f81902" />
</p>
<p>(Observe RDP Traffic)
Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)
Observe the immediate non-stop spam of traffic? Why do you think it’s non-stop spamming vs only showing traffic when you do an activity?

  
  Answer: because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted
</p>
<br />

