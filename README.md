<h1>Built my own SOC</h1>
 
<h2>✍🏿Description</h2>
Built a foundational Security Operations Center lab, set up a C2 framework for emulating threat act behaviour, thrown attacks and cought the detection
<br />


<h2>🧑🏿‍💻Environments Used </h2>

- <b>VMware Workstation</b>
- <b>Windows VM(victim)</b>
- <b>Ubuntu(attacker)</b>

<h2>🚶🏿Walk-through:</h2>
<h3>Part1️⃣ :</h3>

<p align="center">
 
- <b>Installed Sysmon analysis tool in Windows Virtual Machine.</b>
- <b>Installed LimaCharlie EDR on Windows Virtual Machine</b>
- <b>Created account- Created an organization</b>
- <b>Added a Windows VM Lab sensor.</b>
- <b>Disabled all Sysmon and LimaCharlie security</b>

 <br/>
<img src="https://imgur.com/VydJaAK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

- <b>Configured LimaCharlie to ship the Sysmon event logs with its own EDR telemetry-added a new rule.</b>
- <b>Set up an Attack System- using IP address from Linux VM installation process.</b>
- <b>Set up attacker C2 server using Sliver, thi is a Command &  Control (C2) framework by BishopFox.</b>
- <b>Created a working directory for Sliver.</b>

<br />
 <h3>Part2️⃣ :</h3>
 <p align="center">
  
- <b>Generated our C2 payload-</b>
- <b>Launched Sliver in Linux VM</b>
- <b>Generated the first C2 session payload using my own Linux VM IP address</b>
- <b>Downloaded the payload from Linux VM to Windows VM (using pyhton “python3 -m http.server 80”)</b>
- <b>Staged the Malware – by downloading C2 payload from Linux VM to the Windows VM</b>
  
 <br/>
<img src="https://imgur.com/8fbMeyx.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

 - <b>Start Command and Control Session</b>
 - <b>From the Linux VM- I enabled Sliver HTTP server to catch the callback </b>
 - <b>From Windows VM- I executed the C2 payload </b>
 - <b>From the Linux VM- Now I am able to interact directly with the C2 session on the Windows VM</b>
 - <b>I can examine network connections occurring on the remote system (using netstat) and I can identify the running processes on remote system (using ps -T)</b>
   
<br />


- <b>Observing the EDR Telemetry</b>
- <b>By going on LimaCharlie web UI and navigating to the File System tab</b>
- <b>Going to the location of where my implant is running. I will use VirusTotal to scan for suspicious executables</b>
- <b>On the timeline tab, I can filter the timeline using my known IOCs (such as name of my implant or my C2 IP address) and examine events related to implant process.</b>

<img src="https://imgur.com/gxv3BOT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<br />
<h3>Part3️⃣ :</h3>
Dropped into a C2 session on my Windows VM(victim) and ran some commands within the Sliver server on my victim host:

- <b>getprivs-checked the privileges to make sure we can perform privileged actions on the host</b>
- <b>Dumped the lsass.exe process from memo-dump remote process from memory, and saved it locally on my Sliver C2 server</b>
- <b>Detected the telemetry on LimaCharlie by using the Event Type Filters.</b>
- <b>Used EDR to  generate events for detecting "SENSITIVE_PROCESS_ACCESS" targeted  by credential dumping tools. </b>

<img src="https://imgur.com/uQIotag.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

- <b>Created a detection and response rule to alert anytime this activity occurs</b>
- <b>Specified that the detection should only look at the SENSITIVE_PROCESS_ACCESS events with the pocesses ending with lsass.exe</b>

<img src="https://imgur.com/dAGNAAi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

- <b>Going back to my Silver server in my C2 session, run procdump command again then check the detections tab on LimaCharlie menu.</b>
- <b>I can see that I've detected a threat with my own detection signature.</b>

<img src="https://imgur.com/AjrIUme.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<h3>Part4️⃣ :</h3>
Block attacks<br/>

- <b>Getting back SSH onto my Linux VM and dropping into another C2 session on my victim machine</b>
- <b>I then run a command to generate a telemetry (vssadmin delete shadow /all)</b>
- <b>After I use the whoami command to verify I still have an active system shell</b>
- <b>If the rule is successful, the system will not return anything from the whoami command as the process has been terminated.</b>
- <b>Then I check on LimaCharlie’s detection tab to see if the default Sigma rules have picked up the detection. I check the reference URLs for command lines to see the detections.</b>
- <b>I can view the event in the Timeline tab to see the raw event that generated this detection.</b>
- <b>Finally I created a Detection & Response rule from this event.</b>


<img src="https://imgur.com/Xlqa9c0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

