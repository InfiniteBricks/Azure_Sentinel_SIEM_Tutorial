# Azure_Sentinel_SIEM_Tutorial

Azure Sentinel (SIEM) Tutorial - October 2023

 ### [Inspired by this YouTube video](https://www.youtube.com/watch?v=RoZeVbbZ0o0)
 Title:  SIEM Tutorial for Beginners | Azure Sentinel Tutorial MAP with LIVE CYBER ATTACKS!<br>
 Creator: Josh Madakor<br>
 Date of video: November 1, 2021
 
<br>
<h2>Description</h2>

"In this video, I setup Azure Sentinel (SIEM) and connect it to a live virtual machine acting as a honey pot. We will observe live attacks (RDP Brute Force) from all around the world. We will use a custom PowerShell script to look up the attackers Geolocation information and plot it on the Azure Sentinel Map! LEARN THIS IN DEPTH AND PUT THIS ON YOUR RESUME!" --Josh Madakor<br/>
(copied from original YouTube video decription)

Microsoft Azure services have changed since the video's creation on Nov. 2021. After a lot of RTFM and a few Stack Overflow searches, I was able to complete the tutorial and get the desired results.

<br>
<h2>Applications, Languages, Services and Environments Used</h2>

- MS Azure (Free account for 12 month with a $200 account credit)
    - Windows 10 Pro Virtual Machine
    - Log Analytics Workspace    
    - Data Collection Endpoint
    - Data Collection Rule
    - Microsoft Defender for Cloud
    - Network Security Group
    - Microsoft Sentinel
    - Azure Workbook
- Remmina (Remote Desktop Client)
- IP to GEO PowerShell Script (script provided by video creator)
- IP to GEO API (Free ipgeolocation.io account with 1000/day lookups)
- PowerShell
- Nano
- Firefox
- Linux Mint

<br>
<h2>Tutorial Overview</h2>

<p align="left">
 
The virtual machine(screen capture below) has no security defenses and is open/exposed to the internet. The PowerShell script is monitoring the windows event logs for event ID 4625 which is a failed rdp login attempt(larger background window with the latitude & longitude values) and appends these to the custom failed_rdp.log(smaller foreground window with file highlighted) with the geolocation info from the ipgeolocation.io API. <br>
<br>
<img src="/images/win10vm.png" alt="win10vm_screenshot"/>
<br>
<br>
<br>
 
FINAL RESULT = In Microsoft Sentinel the data from the failed_rdp.log is used to plot points on a world map as they happen. The screen capture below shows the geolocations of source ip addresses that attemped to login to the unprotected virtual machine. Login attempts from the United States, South Africa, Australia, Vietnam, France, Russia and India.<br> 
<br>
<img src="/images/world_map.png" alt="world_map_screenshot"/>
<br>

</p>

<br>
<h2>Issues</h2>

1st issues was with the task "Enable gathering VM logs in Security Center". In Azure 2023 Security Center is now MS Defender for Cloud and Pricing & Settings is now Environment Settings.

2nd issue was with the task "Connect Log Analytics to VM". In Azure 2023 the method shown is being replaced with Azure Monitor and Azure Monitor Agent(AMA). Azure Monitor Agent runs on the virtual machine and a data collection rules(DCR) is setup in Log Analytics Workspace to connect to the AMA.

3rd issue was with the task "Create custom fields/extract fields from raw custom log data". In Azure 2023 the method shown is replaced with Tables in Log Analytics Workspace.
