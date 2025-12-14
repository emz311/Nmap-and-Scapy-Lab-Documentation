# Nmap-and-Scapy-Lab-Documentation
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
nmap -v


Nmap version 7.94 Purpose: To verify the installed Nmap version before running any scans.
nmap -sn 10.6.6.0/24

This was performed to know the number of host(s) that are available for use.
sudo nmap -O 10.6.6.23


Identify the operating system by analyzing network responses OS is Linux
## SMB Agressive Enumeration
### Port 21 Aggressive Service Scan
nmap -p21 -sV -A -T4 10.6.6.23


This command identifies the service running on port 21, detects version information, and performs aggressive scanning. Your output should look like below

## SMB Ports Scan (139 and 445)
nmap -A -p139,445 10.6.6.23


Enumerates SMB services and gathers additional OS and network information.

## SMB Share Enumeration with NSE Script
nmap --script smb-enum-shares.nse -p445 10.6.6.23

Detects SMB shares available on the target system
