# Nmap and Scapy Lab Documentation
Practical Lab on network reconnaissance and traffic analysis
This document outlines the procedures for performing host discovery, service enumeration, operating system detection, SMB scanning, packet crafting, packet sniffing, and ICMP traffic analysis within an internal lab network using Nmap and Scapy. The purpose of this lab was to gain hands-on experience with network reconnaissance, service enumeration, and packet analysis
### Lab environment
Operating System: Kali Linux
Tools: Nmap, Scapy, tcpdump
Network Range: 10.6.6.0/24
Target Host: 10.6.6.23
Interface Used: br-internal / eth0
# Nmap Documentation 
# Host Discovery
```bash
nmap -v
```
Nmap version 7.94 Purpose: To verify the installed Nmap version before running any scans.
```bash
nmap -sn 10.6.6.0/24
```
This was performed to know the number of host(s) that are available for use.
```bash
sudo nmap -O 10.6.6.23
```
Identify the operating system by analyzing network responses OS is Linux
# SMB Agressive Enumeration
### Port 21 Aggressive Service Scan
```bash
nmap -p21 -sV -A -T4 10.6.6.23
```
This command identifies the service running on port 21, detects version information, and performs aggressive scanning. Your output should look like below

## SMB Ports Scan (139 and 445)
```bash
nmap -A -p139,445 10.6.6.23
```
Enumerates SMB services and gathers additional OS and network information.

## SMB Share Enumeration with NSE Script
```bash
nmap --script smb-enum-shares.nse -p445 10.6.6.23
```
Detects SMB shares available on the target system
# SMB Client Verification
```bash
smbclient //10.6.6.23/print$ -N
```
Check if anonymous SMB login is allowed
# Wireshark Lab Documentation
### Packet Capture with Wireshark/tcpdump
```bash
pwd              
ifconfig          
cat /etc/resolv.conf  
ip route         
```
To verify network configuration before capturing packets
Packet Capture with tcpdump
```bash
sudo tcpdump -i eth0 -s 0 -w wagwan.pcap
```
Captures all packets passing through the interface during the scans
Stop Capture
```bash
Ctrl + c
```
Verify
```bash
ls wagwan.pcap
```
# Scapy Lab Documentation
### Launch Scapy Environment (Basic Command)
```bash
sudo su        # Run as privileged user,
man scapy      # View Scapy commands
scapy          # Enter the Scapy interactive environment
```
while you are inside scapy
```bash
ls()           # List all available protocols that this tool comes with and can be used
ls(IP)         # View various fields with in an IP packet header 
```
The source tells us where the packet is coming from
to delete a command type clear
### Basic Packet Sniffing
```bash
sniff()         
```
sniff function helps sniff network traffic and observet the traffic
Open a second terminal as the attacker machine 
ping any domain name of your choice
you can use wireshark, it give you the graphicalised view in a form of GUI
```bash
ping google.com
```
to stop capture 
```bash
ctrl + c
```
```bash
ping -c 4 google.com    # c for count and 4 is the number of packets you want to check
```
go to the intial terminal window and type
```bash
ctrl + c
```
sniffed: TCP: 0 UDP: 12 ICMP: 18 Other:4
if you want characters to sign to a vairable, instead of always typing that command from example Wagwan asign W to it, so the network sniffed is a signed to Wagwan
once you type W the program knows that you are referring to Wagwan
Variables serve as containers.
```bash
paro = _            #type this in the terminal were you run the scapy command, _ holds the last command that you run
paro.summary()      # shows the summary of what you sniffed, the command you run earlier
```
### Sniffing on a Specific Network Interface
#### 1. Start network ccapture
sniff (iface = "br-internal")    # specify the interface we want to begin sniffing on
#### 2. Generate interface specific traffic
```bash
ping 10.6.6.1      #  or
10.6.6.23   # then open a browser to start the sniff command of a localy hosted site in the browser
```
#### 3. Stop the sniff capture 
```bash
ctrl + c
```
#### 4. Save the results
```bash
paro2=_          # assign the underscore to paro 2
paro2.summary()  # view the summary
```
you can use wireshark to view in detail
you can also run a command on Nmap to check which devices are present on the network
nmap ip and default getway e.g
nmap 10.6.6.1/24
## ICMP Filtered Sniffing
#### 1. Capture only ICMP packets
```bash
sniff (iface = "br-internal", filter="ICMP", count=10 )   # if you want to limit it to ICMP pacts, with out the filert it gives you everything happening on the network
```
#### 2. Ping ICMP
Ping 10.6.6.23      # run in terminal
or open in a browser 10.6.6.23  # it will not bring iCMP it will use tcp
go back to the previous terminal window end the sniff
```bash
ctrl + c
```
#### 3. Store capture ICMP packets 
Paro4=_           # assign to another variable
paro4.summary()   # view the summary
paro4.nsummary()  # another way to check what happened,a numerical value is assigned to each packets sniffed. helping you concetrate on one packet of your choice
paro4[4]   # the same number from paro summary you used, then a particular line you want to look at
type: ipv4
source IP:10.6.6.23
destination IP:10.6.6.1
source Macaddress:02:42:35:c4:06:d6
destination Macaddress:02:42:0a:06:06:17
this would be an echo reply
The Nmap portion involved discovering active hosts, fingerprinting the target operating system, enumerating services, scanning SMB ports, and verifying SMB access. The Scapy portion demonstrated packet sniffing, interface-based capture, ICMP filtering, and packet inspection. Together, these exercises covered fundamental penetration testing reconnaissance and low-level packet analysis techniques used in real-world cybersecurity operations.
### Ethical Disclaimer
Important: All activities documented here were performed in a controlled, isolated lab environment with explicit authorization. No scanning, packet capture, or network analysis was conducted on public networks or without permission. This work is strictly educational and demonstrates skills for defensive cybersecurity purposes.        
