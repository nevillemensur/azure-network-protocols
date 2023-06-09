<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


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

- Create our Resources
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DNS Traffic
- Observe RDP Traffic

<h2>Actions and Observations</h2>

<p>
  Part 1: Create our resources.
  
1. Create a resource group.
</p>
<p>
<img src="https://i.imgur.com/4pI8KUz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
2. Create a Windows 10 Virtual Machine (VM)
  
  - While creating the VM, select the previously created Resource Group
  
  - While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet
</p>
<p>
<img src="https://i.imgur.com/oFpxhQ7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/afruX6p.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/FRMPBro.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
3. Create a Linux (Ubuntu) VM
  
  - While creating the VM, select the previously created Resource Group and Vnet
</p>
<p>
<img src="https://i.imgur.com/92eVgV3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/y7s6A8E.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/qLnIEtL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
Part 2: (Observe ICMP Traffic)
  
  4. Use Remote Desktop to connect to your Windows 10 Virtual Machine
</p>
<p>
<img src="https://i.imgur.com/FwR1gir.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/mufpOiW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
5. Within your Windows 10 Virtual Machine, Install Wireshark
</p>
<p>
<img src="https://i.imgur.com/Hzm5izC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/WepqwLS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
6. Open Wireshark and filter for ICMP traffic only
</p>
<p>
<img src="https://i.imgur.com/TuDNBc5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
7. Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM

- From The Windows 10 VM, open PowerShell and attempt to ping Ubuntu VM
  
- Observe ping requests and replies within WireShark
</p>
<p>
<img src="https://i.imgur.com/pZEwa1p.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/QeFzUYk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/RWFC15u.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
8. From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark
</p>

<p>
<img src="https://i.imgur.com/yfx5mpu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
9. Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM
  
- Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic
</p>

<p>
<img src="https://i.imgur.com/fwo4OvK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/Zjuc1yS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/277CX3t.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/3tR8CWM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/2HwR5GD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
- Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity
  
</p>

<p>
<img src="https://i.imgur.com/gGXwYPV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
- Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using

</p>
<p>
<img src="https://i.imgur.com/1upP7f1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
- Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)
</p>

<p>
<img src="https://i.imgur.com/f3EtAEp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
- Stop the pinging activity
</p>

<p>
<img src="https://i.imgur.com/3Om3AGw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
11. Back in Wireshark, filter for SSH traffic only
</p>

<p>
<img src="https://i.imgur.com/fzjWprW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
12. From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)
</p>

<p>
<img src="https://i.imgur.com/kbvrZcg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
- Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark

</p>

<p>
<img src="https://i.imgur.com/SuPX3Vk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
- Exit the SSH connection by typing ‘exit’ and pressing [Enter]
</p>

<p>
<img src="https://i.imgur.com/vYmn9mk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
15. Back in Wireshark, filter for DNS traffic only

</p>

<p>
<img src="https://i.imgur.com/xhiEokU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
16. From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are

</p>

<p>
<img src="https://i.imgur.com/dcbhJoO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
17. Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)

  - Observe the immediate non-stop spam of traffic? Why do you think it’s non-stop spamming vs only showing traffic when you do an activity?
 
- Answer: Its because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted

</p>

<p>
<img src="https://i.imgur.com/qL0cQzM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
