<h1>Built my own SOC</h1>

 ### [YouTube Demonstration](https://youtu.be/7eJexJVCqJo)

<h2>Description</h2>
Built a foundational SOC analyst lab, set up a C2 framework for emulating threat act behaviour, thrown attacks and cought the detection
<br />


<h2>Environments Used </h2>

- <b>VMware Workstation</b>
- <b>Windows VM</b>
- <b>Ubuntu/b>

<h2>Walk-through:</h2>
<h3>Part 1:</h3>
<p align="center">
Installed Sysmon in Windows Virtual Machine. Installed LimaCharlie EDR on Windows Virtual Machine- created account- created an organization- added a Windows VM Lab sensor. Disabled all Sysmon and LimaCharlie security: <br/>
<img src="https://imgur.com/IQpjwrO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
 Configured LimaCharlie to ship the Sysmon logs alongside its own EDR telemetry-added a new rule.
Set up an Attack System- using IP address from Linux VM installation process – set up attacker C2 server using Sliver- a Command &  Control (C2) framework by BishopFox.
Created a working directory for Sliver.
<br />
 <h3>Part 2:</h3>
 <p align="center">
Generate our C2 payload-
Launch Sliver in Linux VM
Generate a the first C2 session payload (using own Linux VM IP address
Download the payload from Linux VM to Windows VM (using pyhton “python3 -m http.server 80”)
Stage the Malware – by downloading C2 payload from Linux VM to the Windows VM
 <br/>
<img src="https://imgur.com/JnEvRCj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
  Start Command and Control Session
From the Linux VM-enable Sliver HTTP server to catch the callback 
From Windows VM-execute payload 
From the Linux VM-now able to interact directly with the C2 session on the Windows VM
--can examine network connections occurring on the remote system (netstat), ID running processes on remote system (ps -T)
<br />
<br />
Observe EDR Telemetry
Can filter timeline using my own IOCs(Indicators Of Compromise)-examine events related to implant process. <br/>
<img src="https://imgur.com/jjSfflf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
 Dropped into a C2 session on my victim and ran some commands within the Sliver server on my victim host -- getprivs, dump the lsass.exe process from memo(dump remote process from memory, and save it locally on my Sliver C2 server)
<br />
<h3>Part 3:</h3>
Detect the telemetry on LimaCharlie. Use EDR to  generate events for detecting sensitive process targeted  by credential dumping tools  <br/>
<img src="https://imgur.com/uQIotag.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Crafted a detection and response rule to alert anytime this activity occurs <br/>
<img src="https://imgur.com/dAGNAAi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Return procdump on the Sliver sever console and check the Detection on LimaCharlie, you will see that you have detected a threat with your own detection signature.  <br/>
<img src="https://imgur.com/AjrIUme.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<h3>Part 4:</h3>
Block attacks<br/>
Drop into another C2 session on your victim running a basic command to detect and block (shell)
Run a command to generate a telemetry (vssadmin delete shadow /all)
Run whoami command to verify we still have active system shell
Check LimaCharlie’s detection tab to see if default Sigma picked up the detection – check the reference URLs for command lines to detect.
View event in Timeline to see raw event that generated this detection.
Create a Detection & Response rule from this event.   
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
