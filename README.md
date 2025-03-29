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

- Configure Azure Virtual Network and Virtual Machines
- Configure and Apply Network Security Groups (NSGs)
- Inspect Network Traffic Using Wireshark
- Verify and Monitor Azure Network Activity

<h2>Actions and Observations</h2>

<h3>Configure Azure Virtual Network and Virtual Machines</h3>



















<h2>Actions and Observations</h2>
<h2>Part 1: Create Resources</h2>
<ol>
  <li>Create a Resource Group in Azure.</li>
  <li>Create a Windows 10 Virtual Machine (VM).</li>
  <ul>
    <li>During the VM setup, select the Resource Group created earlier.</li>
    <li>Allow the creation of a new Virtual Network (Vnet) and Subnet for the VM.</li>
  </ul>
  <li>Create a Linux (Ubuntu) Virtual Machine (VM).</li>
  <ul>
    <li>Select the previously created Resource Group and Vnet for this VM.</li>
  </ul>
  <li>Observe the topology and details of your Virtual Network using Azure Network Watcher.</li>
</ol>


<h2>Part 2: Observe ICMP Traffic</h2>
<ol>
  <li>Connect to the Windows 10 VM using Remote Desktop.</li>
  <li>Install Wireshark within the Windows 10 VM.</li>
  <li>Open Wireshark and apply a filter to capture only ICMP traffic (used for ping commands).</li>
  <li>Retrieve the private IP address of the Ubuntu VM and attempt to ping it from the Windows 10 VM.</li>
  <ul>
    <li>Observe the ping requests and replies in Wireshark.</li>
  </ul>
  <li>From the Windows 10 VM, open Command Prompt or PowerShell and ping a public website (such as <code>www.google.com</code>).</li>
  <ul>
    <li>Observe the public ping traffic in Wireshark.</li>
  </ul>
  <li>Initiate a continuous ping from the Windows 10 VM to the Ubuntu VM.</li>
  <li>In the Azure portal, access the Network Security Group (NSG) assigned to the Ubuntu VM and disable inbound ICMP traffic.</li>

<li>Observe how the ICMP traffic stops in Wireshark and the command line due to the blocked traffic.</li>
  </ul>
  <li>Re-enable ICMP traffic in the NSG for the Ubuntu VM.</li>
  <ul>
    <li>Observe the ICMP traffic start working again in Wireshark and on the command line.</li>
  </ul>
  <li>Stop the continuous ping activity from the Windows 10 VM.</li>
</ol>

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

