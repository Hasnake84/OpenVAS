# OpenVAS
## Azure Vulnerability Management

## Objectives
- Set up a secure Azure network with an OpenVAS Vulnerability Management Scanner Virtual Machine
- Deploy a vulnerable Windows 10 VM with outdated software and disable security controls
- Perform credentialed and unauthenticated vulnerability scans using OpenVAS
- Analyze the scan results between unauthenticated and credentialed scans, highlighting the differences
- Remeidiate the identified vulnerabilities
- verify the successful remediation with subsequent scan
  
### Step 1. Prepare Vulnerability Management Scanner
<a href="https://imgur.com/LPv3R3r"><img src="https://i.imgur.com//LPv3R3r.png" title="source: imgur.com" /></a>

### Step 2. Create Client Virtual Machine and Make it Vulnerable
<a href="https://imgur.com/tSrUzSK"><img src="https://i.imgur.com//tSrUzSK.png" title="source: imgur.com" /></a>

1. Disable the Windows Firewall
2. Install an Old Version of FireFox: Firefox Setup 97.0b5
3. Install an Old Version of VLC Player: vlc-1.1.7-win32
4. Install an Old Version of Adobe Reader: 10.0_AdbeRdr1000_en_US_1_
5. Restart the VM.

### Step 3. Configure OpenVAS to Perform First Unauthenticated Scan against the Vulnerable VM
<a href="https://imgur.com/0IoC9MH"><img src="https://i.imgur.com//0IoC9MH.png" title="source: imgur.com" /></a>

1. Added the Client VM PRIVATE IP Address
2. Created new target from the Host
3. Enable Remote Registry
4. Created a new Task
5. Start a scan

### Step 4. Make Configurations for Credentialed Scans on target VM
<a href="https://imgur.com/fAMrBVc"><img src="https://i.imgur.com//fAMrBVc.png" title="source: imgur.com" /></a>

1. Disable Windows Firewall.
2. Disable User Account Control.
3. Enable Remote Registry
4. Set Registry Key:
   - Launch Registry Editor (regedit.exe) in "Run as administrator" mode.
   - Navigate to HKEY_LOCAL_MACHINE hive.
   - Open SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System key.
   - Create a new DWORD (32-bit) value with the following properties:
     - Name: LocalAccountTokenFilterPolicy
     - Value: 1
   - Close Registry Editor.
5. Restart the VM.

### Step 5. Make Configurations for Credentialed Scans (OpenVAS)
<a href="https://imgur.com/x6vgbxo"><img src="https://i.imgur.com//x6vgbxo.png" title="source: imgur.com" /></a>

1. Configure new Credential
2. Allow Insecure Use
3. CLONE Target 
4. Select SMB for the credential

### Step 6. Execute Credentialed Scan against our Vulnerable Windows VM
<a href="https://imgur.com/6DHwTIE"><img src="https://i.imgur.com//6DHwTIE.png" title="source: imgur.com" /></a>

<a href="https://imgur.com/dQFeM1K"><img src="https://i.imgur.com//dQFeM1K.png" title="source: imgur.com" /></a>


### Step 7. Remediate Vulnerabilities
<a href="https://imgur.com/tEJMvlJ"><img src="https://i.imgur.com//tEJMvlJ.png" title="source: imgur.com" /></a>

1. Unistalled the outdated applications 
   - Adobe Reader
   - Mozilla Firefox
   - VLC Mdeia player

### Step 8. Verify Remediations
<a href="https://imgur.com/BefjCZG"><img src="https://i.imgur.com//BefjCZG.png" title="source: imgur.com" /></a>

 Note that there are no longer Vulnerabilities for FireFox, VLC Player, or Adobe Reader!

