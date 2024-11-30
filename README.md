<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

# Networking Lab - Azure Virtual Machines, Packet Analysis, and Network Security
This lab provides hands-on experience with networking concepts using Azure Virtual Machines (VMs) and Wireshark for packet analysis. It covers the creation of VMs, monitoring network traffic, and configuring firewalls in Azure to control and secure traffic.

The exercises emphasize practical networking skills, including the use of ICMP, SSH, DHCP, DNS, and RDP protocols, and demonstrate the importance of tools like Wireshark for troubleshooting and analysis.

---

## Table of Contents
1. [Part 1: Setting Up Virtual Machines](#part-1-setting-up-virtual-machines)
2. [Part 2: Observing Network Traffic with Wireshark](#part-2-observing-network-traffic-with-wireshark)
    - [ICMP Traffic](#icmp-traffic)
    - [Ping to Public Websites](#ping-to-public-websites)
3. [Part 3: Advanced Traffic Observation and Firewall Configuration](#part-3-advanced-traffic-observation-and-firewall-configuration)
    - [Configuring ICMP Firewall Rules](#configuring-icmp-firewall-rules)
    - [Observing SSH Traffic](#observing-ssh-traffic)
    - [Observing DHCP Traffic](#observing-dhcp-traffic)
    - [Observing DNS Traffic](#observing-dns-traffic)
    - [Observing RDP Traffic](#observing-rdp-traffic)
4. [Lab Cleanup](#lab-cleanup)
5. [Networking Best Practices](#networking-best-practices)
6. [Troubleshooting Common Issues](#troubleshooting-common-issues)
7. [Licensing Information](#licensing-information)
8. [Contact Information](#contact-information)

---

## Part 1: Setting Up Virtual Machines

1. **Create a Resource Group**:
   - Navigate to the [Azure Portal](https://portal.azure.com/).
   - Create a new Resource Group to manage your resources for this lab.

2. **Deploy a Windows 10 VM**:
   - Use the new Resource Group when creating the VM.
   - Allow Azure to create a new Virtual Network (VNet) and Subnet for this VM.
   - Use the following credentials for setup:
     - **Username**: `labuser`
     - **Password**: `Cyberlab123!`

3. **Deploy an Ubuntu VM**:
   - Use the same Resource Group and Virtual Network as the Windows 10 VM.
   - Ensure both VMs are in the same Virtual Network and Subnet.
   - Set the authentication type to **Username/Password** and use:
     - **Username**: `labuser`
     - **Password**: `Cyberlab123!`

4. **Verify Connectivity**:
   - From the Windows 10 VM, retrieve the private IP of the Ubuntu VM and ensure they can ping each other.

---

## Part 2: Observing Network Traffic with Wireshark

### ICMP Traffic
1. **Set Up Wireshark**:
   - Install Wireshark on the Windows 10 VM.
   - Start capturing packets.

2. **Ping Ubuntu VM**:
   - From the Windows 10 VM, ping the private IP of the Ubuntu VM:
     ```bash
     ping <Ubuntu-VM-IP>
     ```
   - Observe ICMP packets in Wireshark, including request and reply messages.

### Ping to Public Websites
1. From the Windows 10 VM, use Command Prompt or PowerShell to ping a public website like Google:
   ```bash
   ping www.google.com
   ```
2. Filter the traffic in Wireshark to view the ICMP packets.

---

## Part 3: Advanced Traffic Observation and Firewall Configuration

### Configuring ICMP Firewall Rules
1. **Initiate Continuous Ping**:
   - From the Windows 10 VM, execute a perpetual ping to the Ubuntu VM:
     ```bash
     ping <Ubuntu-VM-IP> -t
     ```

2. **Modify Firewall Rules**:
   - Access the Network Security Group (NSG) for the Ubuntu VM.
   - Disable inbound ICMP traffic.

3. **Observe Traffic Behavior**:
   - Notice in Wireshark that ICMP requests no longer receive replies.
   - Re-enable ICMP traffic in the NSG and verify traffic resumes.

### Observing SSH Traffic
1. **Initiate an SSH Session**:
   - From the Windows 10 VM, open PowerShell and connect to the Ubuntu VM using:
     ```bash
     ssh labuser@<Ubuntu-VM-IP>
     ```
   - Authenticate using the Ubuntu VM's credentials.

2. **Monitor SSH Traffic in Wireshark**:
   - Filter for SSH traffic in Wireshark using the filter:
     ```
     tcp.port == 22
     ```
   - Observe encrypted communication packets.

3. **Exit SSH Session**:
   - Type `exit` and press [Enter].

### Observing DHCP Traffic
1. **Request a New IP Address**:
   - In the Windows 10 VM, run the following command in an elevated Command Prompt or PowerShell:
     ```bash
     ipconfig /renew
     ```
   - Filter for DHCP traffic in Wireshark to observe the IP lease process.

### Observing DNS Traffic
1. **Perform DNS Lookups**:
   - From the Windows 10 VM, use `nslookup` to query domain names:
     ```bash
     nslookup www.google.com
     nslookup www.microsoft.com
     ```
   - Filter for DNS traffic in Wireshark and analyze query and response packets.

### Observing RDP Traffic
1. **Monitor RDP Traffic**:
   - Filter for RDP traffic in Wireshark using the filter:
     ```
     tcp.port == 3389
     ```

2. **Understand Continuous Traffic**:
   - Note the non-stop traffic due to RDP's real-time streaming protocol.

---

## Lab Cleanup

1. Close all Remote Desktop sessions.
2. Delete the Resource Group created during the lab.
3. Confirm that all resources associated with the lab have been removed.

---

## Networking Best Practices

- Always secure VMs with Network Security Groups (NSGs) to limit unwanted traffic.
- Use encryption protocols like SSH for secure remote connections.
- Regularly analyze network traffic for anomalies using tools like Wireshark.
- Implement principle-of-least-privilege for user accounts and NSG rules.

---

## Troubleshooting Common Issues

1. **Issue**: Unable to ping Ubuntu VM from Windows VM.  
   - **Cause**: ICMP traffic blocked by NSG rules.  
   - **Solution**: Ensure ICMP traffic is allowed in the NSG.

2. **Issue**: Wireshark captures no traffic.  
   - **Cause**: Incorrect network adapter selected.  
   - **Solution**: Choose the correct adapter associated with your VM's network interface.

3. **Issue**: SSH connection to Ubuntu VM fails.  
   - **Cause**: SSH traffic blocked by NSG rules.  
   - **Solution**: Allow TCP traffic on port 22 in the NSG.

---

## Licensing Information

Tools used in this lab, including Wireshark, are distributed under their respective licenses. Visit [Wireshark Licensing](https://www.wireshark.org) for details.

---
 
## Contact Information
For questions or feedback, feel free to reach out:  
- **GitHub**: https://github.com/Pieratboi  
- **LinkedIn**: <a href="https://www.linkedin.com/in/rafael-razapov-60391a2b8/?trk=opento_sprofile_topcard"> Rafael Razapov </a>  
