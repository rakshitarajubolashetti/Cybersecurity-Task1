# Cybersecurity Internship Task 1 – Network Scanning using Nmap

## Objective
The objective of this task was to perform network reconnaissance and vulnerability assessment using the Nmap tool. The aim was to identify active hosts, open ports, and running services in my local network, analyze the results, and provide possible security recommendations.

## Steps Performed

1. **Installation**
   - Installed Nmap version 7.98 on my Windows system from the official Nmap website.

2. **Finding Local IP Range**
   - Used the command `ipconfig` in Command Prompt to identify my local IPv4 address and subnet mask.
   - IPv4 Address: 172.20.10.4  
     Subnet Mask: 255.255.255.240  
     Network Range: 172.20.10.0/28

3. **Discovering Active Hosts**
   - Command used:
     ```
     nmap -sn 172.20.10.0/28 -oN alive_hosts.txt
     ```
   - Result: Two active hosts were found – 172.20.10.1 and 172.20.10.4  
   - The output was saved in the file `alive_hosts.txt`.

4. **Scanning for Open Ports**
   - Command used:
     ```
     nmap -sS -T4 172.20.10.1 172.20.10.4 -oN scan_common_ports.txt
     ```
   - This identified open TCP ports on the active hosts. The results are saved in `scan_common_ports.txt`.

5. **Service and Version Detection**
   - Commands used:
     ```
     nmap -sS -sV -T4 172.20.10.1 -oA host_172.20.10.1_full
     nmap -sS -sV -T4 172.20.10.4 -oA host_172.20.10.4_full
     ```
   - This provided detailed information about running services and versions on both hosts.  
   - The results were saved in `.nmap`, `.xml`, and `.gnmap` formats for each host.

## Findings and Analysis

### Host 1: 172.20.10.1
**Open Ports and Services**
| Port | Service | Description | Risk |
|------|----------|-------------|------|
| 21/tcp | FTP | File Transfer Protocol | May allow anonymous login and transmit data in plain text |
| 53/tcp | DNS | Domain Name System service | Possible DNS spoofing or cache poisoning if misconfigured |
| 49152/tcp | Unknown | Dynamic/private port | Could be used by background processes |
| 62078/tcp | iphone-sync | iTunes sync service | Should be restricted to trusted devices |

**Recommendations**
- Disable anonymous FTP or use SFTP for secure file transfer.
- Restrict DNS access to internal systems and enable DNS security features.
- Close unused high-numbered ports.

### Host 2: 172.20.10.4
**Open Ports and Services**
| Port | Service | Description | Risk |
|------|----------|-------------|------|
| 135/tcp | MSRPC | Microsoft Remote Procedure Call | Could be exploited for lateral movement |
| 139/tcp | NetBIOS-SSN | File sharing service | Can expose system information |
| 445/tcp | Microsoft-DS (SMB) | Windows file sharing | Common target for ransomware attacks |
| 1433/tcp | MSSQL | Microsoft SQL Server 2022 | May be vulnerable if weak credentials are used |
| 5357/tcp | HTTPAPI (UPnP) | Windows web services | Can be misused if not properly patched |

**Recommendations**
- Disable SMB and NetBIOS if not required.
- Use strong credentials and restrict SQL Server access.
- Apply the latest Windows updates and patches.
- Restrict RPC access to internal and trusted hosts.

## Output Files
- `alive_hosts.txt` – List of discovered active hosts  
- `scan_common_ports.txt` – Open ports identified for each host  
- `host_172.20.10.1_full.*` – Detailed scan results for Host 1  
- `host_172.20.10.4_full.*` – Detailed scan results for Host 2  
- `screenshot_alive_hosts.png` – Screenshot of host discovery  
- `screenshot_scan_common_ports.png` – Screenshot of common ports scan  
- `screenshot_host_fullscan.png` – Screenshot of full scan result  

## Tools and Environment
- Operating System: Windows 10  
- Tool: Nmap 7.98  
- Optional Tool: Wireshark for packet analysis

## Conclusion
This task helped me understand how to use Nmap for active network scanning and basic vulnerability assessment. I learned how to identify live hosts, open ports, and running services in a network. Based on the scan results, I also identified potential security risks and provided recommendations to mitigate them. This exercise improved my practical knowledge of ethical hacking and network security.

## Author
Name: Rakshita Raju Bolashetti  
Internship: Cybersecurity Internship (Elevate Labs)  
Duration: 45 Days (Remote)  
Task: Network Scanning and Reconnaissance  
Date: October 2025
