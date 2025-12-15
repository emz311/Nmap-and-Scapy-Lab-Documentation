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
man scapy      # View Scapy manual
scapy          # Enter the Scapy interactive environment
```
while you are inside scapy
```bash
ls()           # List all available protocols
ls(IP)         # View IP packet header type
```
to delete a command type clear
The source tells us where the packet is coming from
### Basic Packet Sniffing
```bash
sniff()         
```
sniff function help sniff network traffic like wireshark or tcpdump
to sniff a website open another terminal window and type ping google.com
to cancel requests press ctrl + Z together.

