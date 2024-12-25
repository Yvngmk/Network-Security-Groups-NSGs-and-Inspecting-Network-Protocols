Traffic Examination

Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups.
Environments and Technologies Used
Microsoft Azure (Virtual Machines/Compute)
Remote Desktop
Various Command-Line Tools
Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
Wireshark (Protocol Analyzer)
Operating Systems Used
Windows 10 (21H2)
Ubuntu Server 20.04
High-Level Steps
Observe ICMP Traffic
Observe SSH Traffic
Observe DHCP Traffic
Observe DNS Traffic
Observe RDP Traffic
Actions and Observations
1.) The first thing we are going to do is create a resource group so we can put both of our virtual machines in. Once we have our resource group made we then want to make our first virtual machine. The first virtual machine we are going to make is a Windows 10 vm. Select the resource you made, and then name the virtual machine VM1. Make sure you select Windows 10 Pro, version 22H as the operating system. As for the size of the machine we are going to want atleast 2 vcpus, and 16 gb of memory. Create a username and password of your choosing, and keep the inbound port rules as the default options.

Disk Sanitization Steps


Disk Sanitization Steps


2.) After this step we are going to click on next until we get to the networking page and it should automatically create a virtual network and subnet for us.

Disk Sanitization Steps


Click review and create our VM.

Now that we have created our first VM we are going to go ahead and create our second VM, but this time it will be a Ubuntu Server 20.04 LTS machine. It will be the same process as creating our first machine but instead we are going to switch the SSH public key to password instead.

Disk Sanitization Steps


Disk Sanitization Steps


Click next until we get to the networking page again.

The networking should automatically give us the virtual network from VM1 as well as the subnet.

Disk Sanitization Steps


Click review and create, and it will create our second VM.

2.) Now that we have both virtual machines up and running we are going to connect to our Windows 10 vm using the remote desktop connection app. Once we are connected we are going to go to our browser and download and install Wireshark.

"Wireshark is a free and open-source packet analyzer. It is used for network troubleshooting, analysis, software and communications protocol development, and education."

3.) Open wireshark and filter for ICMP traffic only.

Disk Sanitization Steps


4.) We are going to want to retrieve the private IP address of our Ubuntu VM and then attempt to ping it from within our Windows 10 VM using wireshark. To ping the private IP address of the Ubuntu machine open CMD or Powershell on the Windows machine and type: ping 10.0.0.5 or whatever the private IP address is for your Ubuntu machine.

Disk Sanitization Steps


Disk Sanitization Steps


In either CMD or Powershell ping www.google.com and observe the traffic in wireshark.

5.) We then are going to initiate a non-stop ping from our Windows 10 VM to our Ubuntu VM.

6.) Open the Network Security Group of our Ubuntu machine and disable incoming (inbound) ICMP traffic. To disable incoming ICMP traffic click "Add" new rule and copy everything exactly from the picture. Once that is done you can create the rule and it will create automatically and show up as a new rule.

Disk Sanitization Steps


Disk Sanitization Steps


Now that we have disabled incoming ICMP traffic from VM2 if we go back to VM1 you can see the ping request is timing out.

7.) Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working) Stop the ping activity

8.) The next thing we are going to do is Observe SSH Traffic.
