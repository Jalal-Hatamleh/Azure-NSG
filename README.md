<p align="center">
  <img src="https://github.com/Jalal-Hatamleh/Azure-NSG/blob/main/images/1.png?raw=true" alt="Installation Screenshot"/>
</p>

# Traffic Examination and Network Security Groups (NSGs) in Azure

In this home lab project, I worked on examining and analyzing network traffic between Azure Virtual Machines (VMs). I used different network protocols like ICMP, SSH, RDP, DNS, and DHCP to capture and inspect traffic. The goal was to understand how traffic flows, use Wireshark for packet capture, and explore the role of Network Security Groups (NSGs) in controlling traffic within Azure environments. Below are the steps I followed and the observations I made during the process.

## Environments and Technologies Used

- **Microsoft Azure** (for creating and managing Virtual Machines)
- **Remote Desktop (RDP)** (for connecting to VMs)
- **Wireshark** (for traffic analysis)
- **PowerShell** (for traffic monitoring)
- **Linux (Ubuntu Server 20.04)**
- **Windows 10 (21H2)**

## Step-by-Step Walkthrough

### Part 1: Creating Resources

1. **Create a Resource Group**  
   First, I created a new Resource Group in Azure to keep all the resources in one place and organized.

2. **Create a Windows 10 Virtual Machine (VM)**  
   Next, I created a Windows 10 VM and made sure to assign it to the Resource Group I just created.

   ![Create Windows 10 VM](image-path)

3. **Create a Virtual Network (Vnet) and Subnet**  
   While creating the VM, I allowed the creation of a new Virtual Network and Subnet so that the VMs could communicate with each other.

   ![Vnet and Subnet](image-path)

4. **Create a Linux (Ubuntu) Virtual Machine**  
   After the Windows VM was set up, I created an Ubuntu VM in the same Resource Group and VNet, ensuring that the two machines could talk to each other.

   ![Create Ubuntu VM](image-path)

5. **Check Network Configuration with Network Watcher**  
   To make sure everything was set up correctly, I used Azure's **Network Watcher** to confirm that the network configurations were all in place.

   ![Network Watcher](image-path)

### Part 2: Observing ICMP Traffic

1. **Connect to the Windows 10 VM**  
   I connected to the Windows 10 VM using **Remote Desktop**.

   ![Windows 10 Remote Desktop](image-path)

2. **Install Wireshark on Windows 10 VM**  
   I installed **Wireshark** on the Windows 10 VM to capture network traffic.

   ![Wireshark Installation](image-path)

3. **Filter for ICMP Traffic in Wireshark**  
   Opened Wireshark, set a filter for **ICMP traffic**, and started capturing to see how ping requests and replies behave.

   ![Wireshark ICMP Filter](image-path)

4. **Ping the Ubuntu VM**  
   I found the private IP address of the Ubuntu VM and pinged it from Windows 10, watching the ICMP traffic in Wireshark.

   ![Ping Ubuntu VM](image-path)

5. **Ping a Public Website**  
   I also pinged **www.google.com** from the Windows 10 VM and observed the ICMP traffic in Wireshark.

   ![Ping Google](image-path)

6. **Perpetual Ping**  
   To generate more continuous traffic, I used the command `ping -t` to ping the Ubuntu VM non-stop and saw the traffic in Wireshark.

   ![Continuous Ping](image-path)

7. **Block ICMP Traffic with NSG**  
   I went into the **Network Security Group (NSG)** associated with the Ubuntu VM and blocked incoming ICMP traffic to see what happened.

   ![Block ICMP NSG](image-path)

8. **Observe the Impact**  
   Once the traffic was blocked, I went back to the Windows 10 VM and noticed that the ping requests stopped showing up in Wireshark.

9. **Re-enable ICMP Traffic**  
   After re-enabling ICMP traffic in the NSG, I observed the ping traffic resumed in Wireshark.

   ![Re-enable ICMP NSG](image-path)

10. **Stop the Ping Activity**  
   Finally, I stopped the perpetual ping to finish the observation.

### Part 3: Observing SSH Traffic

1. **Filter for SSH Traffic in Wireshark**  
   I then switched to monitoring **SSH traffic** by setting the appropriate filter in Wireshark.

   ![Wireshark SSH Filter](image-path)

2. **SSH into Ubuntu VM from Windows 10**  
   I connected to the Ubuntu VM via SSH from the Windows 10 VM using the private IP address and ran some basic commands.

   ![SSH Connection](image-path)

3. **Watch SSH Traffic**  
   I observed how the SSH traffic appeared in Wireshark as I interacted with the Ubuntu VM.

   ![SSH Command Interaction](image-path)

4. **Exit the SSH Session**  
   After I was done with the session, I exited SSH by typing `exit` and observed how the traffic stopped.

### Part 4: Observing DHCP Traffic

1. **Filter for DHCP Traffic in Wireshark**  
   I set Wireshark to capture only **DHCP traffic** to understand how the Windows 10 VM obtained its IP address.

   ![Wireshark DHCP Filter](image-path)

2. **Renew the IP Address**  
   I ran the command `ipconfig /renew` on the Windows 10 VM to request a new IP address and captured the DHCP traffic.

   ![IP Renew](image-path)

### Part 5: Observing DNS Traffic

1. **Filter for DNS Traffic in Wireshark**  
   I filtered for **DNS traffic** in Wireshark to see how name resolution requests and responses were handled.

   ![Wireshark DNS Filter](image-path)

2. **Use nslookup in Windows 10**  
   I ran the `nslookup` command on Windows 10 to resolve a domain name to an IP address and captured the DNS traffic.

   ![nslookup](image-path)

### Part 6: Observing RDP Traffic

1. **Filter for RDP Traffic in Wireshark**  
   I filtered for **RDP traffic** (port 3389) in Wireshark to see what the traffic looked like during a remote desktop session.

   ![Wireshark RDP Filter](image-path)

2. **Observe RDP Traffic**  
   I connected to the Windows VM remotely using RDP and observed the constant traffic in Wireshark. Unlike SSH, RDP traffic is continuous because it streams the live display of the desktop.

   ![RDP Traffic](image-path)

### Key Takeaways and Skills Developed

Through this lab, I gained hands-on experience with network traffic analysis and security in Azure. Some of the key skills I developed include:

- **Traffic Filtering**: Filtering traffic by protocols such as ICMP, SSH, DNS, RDP, and DHCP using Wireshark.
- **Network Security Groups (NSGs)**: Configuring and testing NSGs to control traffic flow between VMs and observing how they impact network communication in real-time.
- **VM Configuration**: Creating and configuring both Windows and Ubuntu VMs in Azure and ensuring they could communicate across networks.
- **Real-Time Traffic Monitoring**: Using Wireshark to capture and analyze live traffic for various network protocols, providing insights into their behavior.
- **Security Implementation**: Blocking and allowing specific types of traffic (e.g., ICMP, SSH) using NSGs and observing the effects on the network traffic.

This hands-on experience enhanced my understanding of network protocols, security measures, and real-time traffic analysis, all crucial skills in cloud network security and infrastructure management.
