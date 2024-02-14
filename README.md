<h1>Threat Hunting</h1>


<h2>Project Summary</h2>

The aim of this project is to hunt for any presence of the malware in a system. A disk image was taken. I have to collect Indicators of compromise (IOCs) from two malware samples and to generate two IOC files using Mandiant IOC Editor. Then I have to use these IOC files to audit the disk image using Redline. The project involves real malwares. I was provided with two strings which I need to include in my IOCs: 390808010001Z0U1, #H3XGROUPWASHERE


 

<h2>Skills Achieved</h2>

  - <b> Generating IOC using Mandiant IOC editor</b>
  - <b> Malware Threat hunt by IOCs using Redline</b>


<h2>Tools/software  Used </h2>

- <b> Mandiant IOCe</b>
- <b> Redline</b>
- <b> PowerShell</b>

<h2>Project walk-through:</h2>

<p align="center">
<br/>
This whole project is completed in three steps:

 At first step: I have collected all different types of IOCs such as  MD5, SHA1, SHA256 Hashes; File Size, File Name, Strings from real malwares.

 At second step: I generated IOC files using Mandiant IOC editor using these IOCs

 At the third stage, I have analyzed my Target disk image based on these two IOC files using Redline.

Please check below the image of the real malware files:  <br/>

<img src="https://github.com/msislam23/ThreatHunting/assets/157939065/30bcdeff-44eb-4119-880d-0302ef09ec82"/>
<br />

<p align="center">
<br />
Collecting IOCs:  <br/>

 - <b>File name and Size:
    For windows these are very easy to collect, just right click on the file, go to Properties, and copy the filename and file size. For my case I have used 2 malware samples to collect these information. <br />
    
    <img src="https://github.com/msislam23/ThreatHunting/assets/157939065/66ecec0c-03a4-4ef4-9eb7-730e657f328a"/>
    <br />
 - <b>File Hashes:
    I have created MD5, SHA1 and SHA256 checksums, which can be used as a file hash indicator to search for the exact same file on a system. To retrieve file hashes in Windows, I opened the windows PowerShell terminal and moved into     the same location as the file I  wanted to retrieve the hash for, and used the command "Get-FileHash <filename>".By default the algorithm creates SHA256 checksum. For generating MD5 and SHA1, I used "-algorithm" flag to specify      MD5 or SHA1. <br />
    
    <img src="https://github.com/msislam23/ThreatHunting/assets/157939065/2b7574cb-c195-40f4-b4d8-4f9f3c777604"/>
    <br />
 - <b>File Strings:
    I used all strings provided by threat intelligence team. 
    STRINGS: 390808010001Z0U1, #H3XGROUPWASHERE 
    <br />
    <p align="center">
    <br />
    The entire IOC summary is below: 
    <img src="https://github.com/msislam23/ThreatHunting/assets/157939065/ac42c058-c556-4f40-85b9-b852e5e5dc9b"/>
    <br />
 
<p align="center">
<br />
 Creating IOC files using Mandiant IOC editor: <br/>
 
 For creating IOC files, I created a folder in my desktop location-C:\Users\sha\Desktop\IOCs.

 After opening Mandiant IOCe, select the newly created folder and press ok. The file path is visible at the top of the window.

<img src="https://github.com/msislam23/ThreatHunting/assets/157939065/0eb4046d-df64-41cd-ba6d-e40438d8ef84"/>


<img src="https://github.com/msislam23/ThreatHunting/assets/157939065/caa21d62-ca8a-45a6-9d4c-eb7993d632bf"/>
<br />
<br />
Now to create an IOC file, select File > New > Indicator.<br/>

<img src="https://github.com/msislam23/ThreatHunting/assets/157939065/f09c52a7-8038-45f3-b833-9a831d9094ee"/>
<br />
<br />
Properly fill up the fields such as name, Author, Description etc.<br/>

<img src="https://github.com/msislam23/ThreatHunting/assets/157939065/6d80cb2e-b311-4486-8a65-a416d2684cf5"/>
<br />
<br />
Right-click anywhere in the bottom pane and go to Add Item > FileItem and select all relevant items such as MD5, SHA1, SHA256, File size, Name, Strings as IOC.

 
 SHA-1 Hash: Add Item > FileItem > Sha1sum
 
 File Name: Add Item > FileItem > File Name
 
 File Size: Add Item > FileItem > File Size

This creates a new entry in our OR tree.

<img src="https://github.com/msislam23/ThreatHunting/assets/157939065/587ce830-cf23-4da4-b164-cb81fe50ba30"/>

<br />
<br />
After all of the entries, the IOC file is ready, and it looks like as below. I saved the file by clicking save button at the bottom right corner. This way I created both IOC files.

IOC file 1:

<img src="https://github.com/msislam23/ThreatHunting/assets/157939065/6fac6762-0cc5-4320-88f3-00e4569ea283"/>

IOC file 2:

<img src="https://github.com/msislam23/ThreatHunting/assets/157939065/63421d0e-e3fc-4dc7-998a-c286871df6cd"/>
<br />

<p align="center">
<br />
 Hunting for malware based on IOCs created by Redline: <br/>
 
 In this part I will audit a system using redline using our IOC files to identify any presence of any of them in the system.

 After installation of redline and before opening the software, I created a new folder for my IOC collector at-C:\Users\sha\Desktop\THREAT HUNT

 Then open Redline, and select Create an IOC Search Collector

<img src="https://github.com/msislam23/ThreatHunting/assets/157939065/35b42a8b-0b20-4c30-8013-790b6ea7a43e"/>

<br />
<br />
Evidence 4 of 4:<br/>
This was hidden inside the "/J Harrison Disk Image 10.09.2019/WebDev work/unfinished webpages/templatemo_508_power/css".
I used "file" and "strings" commands to find the evidence in kali linux.

<img src="https://github.com/msislam23/DigitalForensics/assets/157939065/a59ee24f-9701-4a85-9ce7-3c992cae3342"/>
<br />
This is personal information of Colin Andrews
<br />
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
