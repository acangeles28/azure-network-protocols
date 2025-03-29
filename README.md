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

<h2>Steps and Objectives</h2>

- Configure Azure Virtual Network and Virtual Machines
- Configure and Apply Network Security Groups (NSGs)
- Inspect Network Traffic Using Wireshark
- Verify and Monitor Azure Network Activity

<h2>Actions and Observations</h2>
<p>Part 1: Create Resources</p>

  - Create a Resource Group and a Windows 10 Virtual Machine (VM) in Azure
  - Allow the creation of a new Virtual Network (Vnet) and Subnet for the VM.
![create VM](https://github.com/user-attachments/assets/bf689278-fc9e-43ba-a446-4e0fbe2805b1)

  - Create a Linux (Ubuntu) Virtual Machine (VM)
    - Select the previously created Resource Group and Vnet for this VM
![ubuntu vm](https://github.com/user-attachments/assets/3fc90842-c7ca-46c9-a309-93bfcec91669)

  - Observe the topology and details of your Virtual Network using Azure Network Watcher
![network topology](https://github.com/user-attachments/assets/15d263b4-1da7-49d8-95a3-b4577e304e5f)

<p>Part 2: Observe ICMP Traffic<p/>

  - Connect to the Windows 10 VM using Remote Desktop
  - Install Wireshark within the Windows 10 VM
  - Open Wireshark and apply a filter to capture only ICMP traffic (used for ping commands).
  - Retrieve the private IP address of the Ubuntu VM and attempt to ping it from the Windows 10 VM.
![ubuntu vm](https://github.com/user-attachments/assets/78935f6c-dfa0-407a-89e5-9e6db86ba7e2)

  - Observe the ping requests and replies in Wireshark.
    
![ping icmp 1](https://github.com/user-attachments/assets/1100c09f-74c8-4886-b18a-aa5e9b5488f4)
  - From the Windows 10 VM, open Command Prompt or PowerShell and ping a public website (such as www.google.com)
  - Observe the public ping traffic in Wireshark
![ping google](https://github.com/user-attachments/assets/f7e85623-378d-4d22-af00-5146a62c73f8)

  - Initiate a continuous ping from the Windows 10 VM to the Ubuntu VM
  - In the Azure portal, access the Network Security Group (NSG) assigned to the Ubuntu VM and disable inbound ICMP traffic
![inbound icmp](https://github.com/user-attachments/assets/dbdfb5b5-93e9-45bb-b167-7a88ba031533)

  - Observe how the ICMP traffic stops in Wireshark and the command line due to the blocked traffic.
<img width="1275" alt="ping icmp timeout" src="https://github.com/user-attachments/assets/eed6d59c-04f3-4631-97d2-bbcf2421bb00" />

  - Re-enable ICMP traffic in the NSG for the Ubuntu VM
![reenable inbound icmp](https://github.com/user-attachments/assets/24bbbaa6-75df-4e99-aa42-aabdba9c3de6)

  - Observe the ICMP traffic start working again in Wireshark and on the command line.
  - Stop the continuous ping activity from the Windows 10 VM.


<h2>Part 3: Observe SSH Traffic</h2>
<ol>
  <li>In Wireshark, apply a filter to capture SSH traffic.</li>
  <li>From the Windows 10 VM, establish an SSH connection to the Ubuntu VM using its private IP address.</li>
  <ul>
    <li>Type commands (e.g., username, password) into the SSH session and observe the SSH traffic in Wireshark.</li>
    <li>Exit the SSH session by typing <code>exit</code> and pressing Enter.</li>
  </ul>
</ol>

<h2>Part 4: Observe DHCP Traffic</h2>
<ol>
  <li>In Wireshark, apply a filter to capture DHCP traffic.</li>
  <li>From the Windows 10 VM, attempt to request a new IP address using the command <code>ipconfig /renew</code>.</li>
  <ul>
    <li>Observe the DHCP traffic in Wireshark as the VM communicates with the DHCP server to renew its IP address.</li>
  </ul>
</ol>

<h2>Part 5: Observe DNS Traffic</h2>
<ol>
  <li>In Wireshark, apply a filter to capture DNS traffic.</li>
  <li>From the Windows 10 VM, use the <code>nslookup</code> command to resolve the IP addresses of websites like <code>google.com</code> and <code>disney.com</code>.</li>
  <ul>
    <li>Observe the DNS query and response traffic in Wireshark.</li>
  </ul>
</ol>

<h2>Conclusion</h2>
<p>In this lab, we explored different types of network traffic between two Azure Virtual Machines, using Wireshark to analyze protocols such as ICMP, SSH, DHCP, and DNS. We also experimented with Network Security Groups to control the flow of ICMP traffic and observed how security settings can affect network behavior. By completing these exercises, we gained insight into how network traffic flows between virtual machines in Azure and how network security controls can be implemented to manage this traffic effectively.</p>

