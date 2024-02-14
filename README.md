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
Click “Browse” in the top right corner and Select the folder where IOC files are located. Select IOC files in the left-hand window, then click “Next” in the bottom right corner.

<img src="https://github.com/msislam23/ThreatHunting/assets/157939065/4bd8b0ef-c5d8-45e9-8fbc-12c6bae1be99"/>
<br />

<br />
Then click Edit your script, Under Disk select the boxes that are relevant for this hunt.

<img src="https://github.com/msislam23/ThreatHunting/assets/157939065/49f73080-1829-45d8-8b3f-c0f2da455800"/>
<br />

<br />
To prevent Redline from scanning entire system looking for target files, select the path where Redline will start searching from. In my case I have put my target directory at my desktop and I will show redline only to look for that location. 

This can be done by navigating to disk tab and selecting “show advanced parameter.”

Edit the Path value with the full file path of my target directory and click ok at the bottom right corner. Now Redline won’t spend ages scanning whole system.

<img src="https://github.com/msislam23/ThreatHunting/assets/157939065/1e5e3e5f-cf1e-4987-ae22-5ea8fdd4de5c"/>
<br />

<br />
Now select a location to save IOC Collector as Redline requires a base location to save all of its files and results from the hunt. Click the “Browse” button at the bottom right and select the new folder as the folder I created before for IOC Search Collector. A popup will confirm that the Collector package has been created and saved to the location selected.

<img src="https://github.com/msislam23/ThreatHunting/assets/157939065/398c90e7-c483-457d-90d2-5aee0a078f89"/>
<br />

<br />
After selecting IOC files and IOC collector base, hunting folder should show all the collector’s files as shown below:

<img src="https://github.com/msislam23/ThreatHunting/assets/157939065/a7668f53-2088-4f79-8021-4d1cfd38254e"/>
<br />

<br />
To start audit, start CMD as administrator. Navigate to the hunting folder in the same location as the collector files and use the command ".\RunRedlineAudit.bat".

<img src="https://github.com/msislam23/ThreatHunting/assets/157939065/16861199-600b-4a33-9245-24d7636f01c7"/>
<br />

<br />
Redline will start audit and create a new directory appear in the Collector folder named “Sessions“, a sub-folder named “AnalysisSession1“, and a file sub-folder called “Audits“.

<img src="https://github.com/msislam23/ThreatHunting/assets/157939065/ccec43e1-35af-4a61-aba8-d990f2f0ef73"/>
<br />

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
