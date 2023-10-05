<h1>Built my own SOC</h1>
 
<h2>✍🏿Description</h2>
Built a foundational Security Operations Center lab, set up a C2 framework for emulating threat act behaviour, thrown attacks and cought the detection
<br />


<h2>🧑🏿‍💻Environments Used </h2>

- <b>VMware Workstation</b>
- <b>Windows VM</b>
- <b>Ubuntu</b>

<h2>🚶🏿Walk-through:</h2>
<h3>Part1️⃣ :</h3>

<p align="center">
 
- <b>Installed Sysmon in Windows Virtual Machine.</b>
- <b>Installed LimaCharlie EDR on Windows Virtual Machine</b>
- <b>Created account- Created an organization</b>
- <b>Added a Windows VM Lab sensor.</b>
- <b>Disabled all Sysmon and LimaCharlie security</b>

 <br/>
<img src="https://imgur.com/IQpjwrO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

- <b>Configured LimaCharlie to ship the Sysmon logs alongside its own EDR telemetry-added a new rule.</b>
- <b>Set up an Attack System- using IP address from Linux VM installation process.</b>
- <b>Set up attacker C2 server using Sliver- a Command &  Control (C2) framework by BishopFox.</b>
- <b>Created a working directory for Sliver.</b>

<br />
 <h3>Part2️⃣ :</h3>
 <p align="center">
  
- <b>Generate our C2 payload-</b>
- <b>Launch Sliver in Linux VM</b>
- <b>Generate a the first C2 session payload (using own Linux VM IP address</b>
- <b>Download the payload from Linux VM to Windows VM (using pyhton “python3 -m http.server 80”)</b>
- <b>Stage the Malware – by downloading C2 payload from Linux VM to the Windows VM</b>
  
 <br/>
<img src="https://imgur.com/JnEvRCj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

 - <b>Start Command and Control Session</b>
 - <b>From the Linux VM-enable Sliver HTTP server to catch the callback </b>
 - <b>From Windows VM-execute payload </b>
 - <b>From the Linux VM-now able to interact directly with the C2 session on the Windows VM</b>
 - <b>can examine network connections occurring on the remote system (netstat), ID running processes on remote system (ps -T)</b>
   
<br />
<br />

- <b>Observe EDR Telemetry</b>
- <b>Can filter timeline using my own IOCs(Indicators Of Compromise)-examine events related to implant process.</b>

<img src="https://imgur.com/jjSfflf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
Dropped into a C2 session on my victim and ran some commands within the Sliver server on my victim host 

- <b>getprivs-check the privileges to make sure we can perform privileged actions on the host</b>
- <b>Dump the lsass.exe process from memo-dump remote process from memory, and save it locally on my Sliver C2 server)</b>

<br />
<h3>Part3️⃣ :</h3>

- <b>Detect the telemetry on LimaCharlie.</b>
- <b>Use EDR to  generate events for detecting sensitive process targeted  by credential dumping tools. </b>

<img src="https://imgur.com/uQIotag.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

- <b>Crafted a detection and response rule to alert anytime this activity occurs</b>

<img src="https://imgur.com/dAGNAAi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

- <b>Return procdump on the Sliver sever console and check the Detection on LimaCharlie.</b>
- <b>Detected a threat with your own detection signature.</b>

<img src="https://imgur.com/AjrIUme.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<h3>Part4️⃣ :</h3>
Block attacks<br/>

- <b>Drop into another C2 session on your victim running a basic command to detect and block (shell)</b>
- <b>Run a command to generate a telemetry (vssadmin delete shadow /all)</b>
- <b>Run whoami command to verify we still have active system shell</b>
- <b>Check LimaCharlie’s detection tab to see if default Sigma picked up the detection – check the reference URLs for command lines to detect.</b>
- <b>View event in Timeline to see raw event that generated this detection.</b>
- <b>Create a Detection & Response rule from this event.</b>

<img src="https://imgur.com/Xlqa9c0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
