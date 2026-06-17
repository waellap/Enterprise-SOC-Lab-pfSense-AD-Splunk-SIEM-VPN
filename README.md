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

Firewall: pfSense
SIEM: Splunk
Directory Services: Active Directory (Windows Server)
Endpoint: Windows Client
VPN: pfSense OpenVPN / IPSec
Network Segmentation: LAN / OPT1 / VPN



## Log Sources (SOC VIEW)
Splunk collects logs from:

 Windows Security Logs (Event Logs)
 Authentication logs (AD)
 VPN connection logs
 Firewall logs (pfSense)
 Network traffic metadata


## Detection Use Cases
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



<img src="https://imgur.com/oBWor6Q.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><img src="https://imgur.com/qUTCQrW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><img src="https://imgur.com/5cR54n5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


<br />
<br />


-Creating the honeypot, which will be Windows 10.

<img src="https://imgur.com/casE3Ic.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><img src="https://imgur.com/DnBGFgk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br />
<br />


-Now we created everything which we the network security group is the firewall, network interface, and ethernet port.

<img src="https://imgur.com/9ci2vJG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />


-I add inbound traffic,  which can receive traffic from any any.


<img src="https://imgur.com/g700mVm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />


Log in to Windows 10, aka (Honeypot).


<img src="https://imgur.com/YTwr0rc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />


-Turning the WF.msc or the Windows Firewall off


<img src="https://imgur.com/wA58yIy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
