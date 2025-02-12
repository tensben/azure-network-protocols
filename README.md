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

![Screenshot 2024-12-18 115523](https://github.com/user-attachments/assets/095e3f37-398c-4adb-bb4d-30cc49ae56b2)

![Screenshot 2024-12-18 115600](https://github.com/user-attachments/assets/82f0b7f6-40a2-4a22-8c9a-af6259004d43)

</p>
<p>
Next, we will observe SSH traffic only using Wireshark on Windows Virtual Machine. SSH is used to make a secure connection from one computer to another. We will use a Windows VM to create an SSH connection to the Linux VM and then observe the traffic. Type ssh in Wireshark to start a capture. Open Windows Powershell and type ssh labuser@<private IP address>. For example, you would type in the Powershell ssh labuser@10.0.0.5.  
</p>
<br />

<p>

![Screenshot 2024-12-18 121247](https://github.com/user-attachments/assets/5b9bca0b-2200-4c43-9524-2ce00f19ca71)

![Screenshot 2024-12-18 121323](https://github.com/user-attachments/assets/57f97f1c-9d1d-4a0c-afca-c4f61555423b)

</p>
<p>
You will observe the SSH traffic in Wireshark when you enter the command line. They will ask if you want to continue connecting. Type yes. Then, you will be prompted to enter the password for the Linux virtual machine you created earlier. The password will not show when you start typing it for security reasons. Once you are finished typing the password, hit enter. You will see more SSH traffic happening in Wireshark. At the end of the Powershell labuser@linux-vm:~$, you are now connected to a Linux VM using SSH.  
</p>
<br />
<p>

![Screenshot 2024-12-18 121427](https://github.com/user-attachments/assets/9f6b5d22-e632-4fe0-8297-a434fe5bc014)

![Screenshot 2024-12-18 121323](https://github.com/user-attachments/assets/a226841f-f36c-4b15-99c6-68f382112a0c)

![Screenshot 2024-12-18 121847](https://github.com/user-attachments/assets/67d85f9b-672e-4ae8-9fe8-f17218d59829)

Anything that is typed will be encrypted, and it is scrambled.
 
</p>
<p>
 
![Screenshot 2024-12-18 122023](https://github.com/user-attachments/assets/171167c1-fa78-4711-bf40-dd0bf1605663) 
</p>
<br />
<p>
To filter TCP traffic, type in Wireshark tcp.port == 22. Then, in Powershell, you type anything in the command line and observe the TCP traffic in Wireshark. Instead of typing SSH, you can type in tcp.port == 22 for the whole filter. To drop the connection to linux -vm, type in exit in Powershell.    
</p>
<br />
<p>
  
 ![Screenshot 2024-12-18 123322](https://github.com/user-attachments/assets/3d2c8a15-43ee-403b-b243-117f027eb444)
 
</p>
<br/>
<p>
In Wireshark, we are going to filter for DHCP traffic only. Dynamic Host Configuration Protocol (DHCP) works on ports 67  and 68 to assign an IP address to devices when they are first connected to the network. In Wireshark, type in DHCP, then in Windows Powershell, type in ipconfig /renew. You will see that we capture DHCP traffic.  
</p>
<br />
<p>

![Screenshot 2024-12-18 124349](https://github.com/user-attachments/assets/4d773e3e-e998-49ba-9b09-b89bc1d41271)

![Screenshot 2024-12-18 124425](https://github.com/user-attachments/assets/a4bd673f-db4b-46b8-b8e1-a9c10a4b7c07)
  
</p>
<p>
Now, in Wireshark, we will filter for DNS traffic only. From the Windows 10 VM PowerShell, type nslookup disney.com, hit enter, and it will show us the Disney IP address. In Wireshark, a lot of spam happens in the back end.  
</p>
<br/>
<p>

![Screenshot 2024-12-18 130018](https://github.com/user-attachments/assets/26a3f171-d98a-49ef-8f42-c2123ff5043f)

![Screenshot 2024-12-18 130345](https://github.com/user-attachments/assets/c2821864-fd70-43bf-8496-492df9485280)
  
</p>
<p>
The last traffic we will observe is RDP traffic. To access it, type in tcp port ==3389 in Wireshark. We observed nonstop spam traffic because the Remote Desktop Protocol shows a live stream constantly being transmitted from one computer to another.  
</p>
<br/>
<p>

 ![Screenshot 2024-12-18 131042](https://github.com/user-attachments/assets/ca256831-c7b9-4801-818f-f8ad65697440)
 
</p>
