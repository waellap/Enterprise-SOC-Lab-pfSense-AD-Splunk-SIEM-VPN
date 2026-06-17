# Enterprise SOC Lab: pfSense + AD + Splunk SIEM + VPN

## Lab Architecture
<img src="https://imgur.com/h7p3SQV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

## Architecture Overview
This lab simulates a real enterprise network secured and monitored by a SOC team.
#### Components:

-pfSense Firewall
Controls traffic between WAN, LAN, OPT1, and VPN
Enforces security rules and segmentation

-WAN (Internet)
Represents external attackers and real-world traffic

-OPT1 Network (10.10.10.0/24)
Contains a Windows Client
Simulates end-user activity

-LAN Network (10.10.20.0/24)
Hosts critical infrastructure:

-Active Directory (AD Server)
Splunk SIEM
-VPN Network (10.10.30.0/24)
Simulates secure remote access users


## Objective
The goal of this lab is to:

Simulate a real corporate network environment
Monitor user and network activity using Splunk SIEM
Detect suspicious or malicious behavior
Practice SOC analysis and threat detection

##  technologies Used

-Firewall: pfSense
-SIEM: Splunk
-Directory Services: Active Directory (Windows Server)
-Endpoint: Windows 10,7 Client
-VPN: pfSense OpenVPN / IPSec
-Network Segmentation: LAN / OPT1 / VPN



## Log Sources (SOC VIEW)
Splunk collects logs from:

 Windows Security Logs (Event Logs)
 Authentication logs (AD)
 VPN connection logs
 Firewall logs (pfSense)
 Network traffic metadata


## Detection Use Cases(Loading)
1.  Brute Force Login (AD)
Detect repeated failed login attempts:
index=windows EventCode=4625
| stats count by src_ip, Account_Name
| where count > 10


2.  Successful Login After Failures
index=windows (EventCode=4625 OR EventCode=4624)
| stats count by src_ip, Account_Name, EventCode


3.  Suspicious VPN Activity
index=vpn
| stats count by src_ip
| sort -count


4.  Firewall Denied Traffic (pfSense)
index=firewall action=blocked
| stats count by src_ip, dest_ip


5.  Privilege Escalation Detection
index=windows EventCode=4672
### Example Log:
##  Steps
Lab photo demonstration.
- Pfsense Firewall (Network Segmentation, Rules, and,VPN)

<img src="https://imgur.com/S4oj092.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><img src="https://imgur.com/imDT0tq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><img src="https://imgur.com/XHTCDsN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><img src="https://imgur.com/TnXXBXr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


<br />
<br />


-VPN Client Windows 10.

<img src="https://imgur.com/Y97mhVi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br />
<br />


-Active Directory Corp.local and It's client Windows 10,7(FANZA=users)

<img src="https://imgur.com/QBqvPHV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><img src="https://imgur.com/HWxGOfW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><img src="https://imgur.com/4wEXtHa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><img src="https://imgur.com/k5Z1c34.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br />
<br />

-Windows 10 Corp.local
<img src="https://imgur.com/1Com48O.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


<br />
<br />


-Splunk.

<img src="https://imgur.com/K6gCzDt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://imgur.com/OVStTTK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/FRZS47P.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br />
<br />


