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

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Actions and Observations</h2>

<p>
This will be a guide on Network Security Groups and Inspecting Network Traffic. First, we must set up two Virtual Machines(VM) - one  Windows virtual machine and one Linux virtual machine. Both machines must have a minimum of two CPUs and must be in the same resource group, region, and Vnet. Once you are finished setting up your virtual machines, deploy the Windows virtual machine and download Wireshark, a powerful network protocol analyzer. Once installed, launch Wireshark and select the Ethernet, then click on the shark fin in the upper left corner to start capturing network traffic for the backend of the Windows virtual machine.  
  
![Screenshot 2024-12-18 111558](https://github.com/user-attachments/assets/2369456a-6a01-4025-b8f4-13a9637786b9)

![Screenshot 2024-12-18 111755](https://github.com/user-attachments/assets/40fb5ef4-3af7-4475-ba89-c817d58fef54)

</p>
<p>
We will filter out the IMCP traffic exclusively to observe network communications. Ping uses IMCP traffic to test connectivity between two devices.
</p>
<br />

<p>
  
![Screenshot 2024-12-18 112934](https://github.com/user-attachments/assets/6409c18d-ce4e-46c5-a28a-3ea4a898b271)

</p>
<p>
Next, we will obtain the private IP address of the Ubuntu virtual machine (linux -vm) and ping it from within Windows 10 virtual machine. In the Windows Virtual Machine, open Windows PowerShell. We will ping the Linux VM with the Windows PowerShell open - type in the Powershell ping followed by the private IP address from Linux. 

</p>
<br />

<p>

![Screenshot 2024-12-18 112830](https://github.com/user-attachments/assets/f8ae1624-2b81-46af-9a39-f9bf78912105)


</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

As you can see, the reply was from the Linux virtual machine, and the request was from the Windows virtual machine.

</p>
<br />

<p>
  
![Screenshot 2024-12-18 112934](https://github.com/user-attachments/assets/298a4285-fb4a-42fe-b59f-4dba69be1c48)

</p>
<p>
Click on Internet Control Message Protocol in the bottom left corner of Wireshark.  You will see that actual data is being sent via ping.
</p>
<br />

<p>

![Screenshot 2024-12-18 113916](https://github.com/user-attachments/assets/cacdc527-413b-47b9-a341-404c7605cecf)

</p>
<p>
In the next portion of this lab, we will type ping Linux private IP address—t. This command line will continue to ping until we stop it. We will then configure the firewall of the Linux Virtual Machine in the Network Security Group. Once we disable incoming inbound ICMP traffic in the Linux Virtual Machine, we will head back to the Windows Virtual Machine and see that Linux stops replying and that the request times out. This happens because we configure a rule to deny traffic from any source and destination.  When we return to Wireshark, we see only requests, not replies, because no response is found. After all, the firewall is blocking them. 
</p>
<br />

<p>

![Screenshot 2024-12-18 114446](https://github.com/user-attachments/assets/321b23e5-0f07-4e3c-9054-e5eb2ac2e9d3)

![Screenshot 2024-12-18 115418](https://github.com/user-attachments/assets/7f111f86-2d86-4655-a6d3-2e6ae61052f3)

![Screenshot 2024-12-18 115146](https://github.com/user-attachments/assets/b5f65d10-5ac6-4635-8dc4-df566db85fc9)

![Screenshot 2024-12-18 115251](https://github.com/user-attachments/assets/7055c2bd-7824-4cb0-9d69-57b43c60f55c)



</p>
<p>
Re-enable IMCP traffic for the Newwork Security Group in the Linux virtual machine. Return to Windows Virtual Machine to observe that IMCP traffic in WireShark and the command line ping activity begin to work again. 
</p>
<br />

<p>
  
</p>
<p>
  
</p>
<br />

<p>
  
</p>
<p>
  
</p>
<br />
<p>
  
</p>
<p>
  
</p>
<br />
