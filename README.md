<p align="center"><img src="https://github.com/alph4w0lf/LokiX/blob/master/lokix-banner.png" width="400"></p>

# LokiX Platform
LokiX Platform is a free open-source solution to help blue teams and threat hunters use "[Loki IOC Scanner](https://github.com/Neo23x0/Loki)" to sweep enterprise networks.

## Features
- Sweep thousands of endpoints concurrently.
- Silent execution.
- Agent deletes itself after completing its sweep.
- Centralized storage for Loki scan results.
- Centralized dashboard to track scans and view scan results.
- Loki update through the platform.
- Auto-highlight of key elements of the scan results.
- IP Spoofing Protection.
- Agent Exception handling and error reporting.

## Supported Systems
#### Currently Supported
- Windows Vista (Need to install .NET Framework version 4.5)
- Windows Server 2008 (Need to install .NET Framework version 4.5)
- Windows 7
- Windows 8
- Windows 10
- Windows Server 2012
- Windows Server 2016
- Windows Server 2019
#### Planned Support (Not available yet)
- Linux Operating Systems
- MacOS

## Installation Steps
#### STEP1: Import LokiX OVA
Download LokiX OVA File: https://github.com/alph4w0lf/LokiX/releases/tag/v1.0

   Extract the 7z compressed file contents (Linux):
```
7z e lokix-virtual-server.7z
```
   Then import it into your favourite virtualization solution.
- [VirtualBox Instructions](https://docs.oracle.com/cd/E26217_01/E26796/html/qs-import-vm.html)
- [VMware vSphere Instructions](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.vsphere.html.hostclient.doc/GUID-8ABDB2E1-DDBF-40E3-8ED6-DC857783E3E3.html)
- [VMware Workstation Instructions](https://docs.vmware.com/en/VMware-Workstation-Pro/15.0/com.vmware.ws.using.doc/GUID-DDCBE9C0-0EC9-4D09-8042-18436DA62F7A.html)
#### STEP2: Configure a Static IP Address (Optional)
Login to LokiX system command line using the OS/SSH Default Credentials:
```
Username: lokix
Password: lokix
```
Then, follow the instructions for setting a STATIC IP on "Ubuntu Server" in this link: 
```https://linuxconfig.org/how-to-configure-static-ip-address-on-ubuntu-20-04-focal-fossa-desktop-server```
Then, perform the following instructions to update the backend configurations with the new IP address:
```
cd /var/www/backend
sudo php artisan config:cache
```
#### STEP3: Firewall Rules (Optional)
```
SOURCE IP                   DESTINATION IP                      PORT                                          REASON
---------------             --------------------                -----------------                             --------------------------
[SCANNED_ENDPOINTS]         [LOKIX_PLATFORM_IP]                 443/tcp (HTTPS)                               For agent<=>platform communication
[LOKIX_PLATFORM_IP]         [INTERNET]                          443/tcp (HTTPS), 53/tcp (DNS)                 For Loki signature updates
```
#### STEP4: Antivirus White-listing (Optional)
```
Type                        Value
--------------              -------------------
FOLDER                      %USERPROFILE%\AppData\Local\Temp\lokix\*
PROCESS                     agent.exe
PROCESS                     loki.exe
```



## Usage Guide
#### Platform Admin Panel Access
- Access the platform through the Web Browser:
```
https://PLATFORM_IP_ADDRESS/
```
  
- Default Credentials:
```
Username: admin@lokix.local
Password: password
```

#### Updating Loki and its Signatures
<p align="center"><img src="https://github.com/alph4w0lf/LokiX/blob/master/screenshots-update.gif?raw=true"></p>


#### Download and Execute the Agent on the Systems that needs to be sweeped
Download LokiX Agent:
<p align="center"><img src="https://github.com/alph4w0lf/LokiX/blob/master/screenshots-download.gif?raw=true"></p>


Execute LokiX Agent:
<p align="center"><img src="https://github.com/alph4w0lf/LokiX/blob/master/screenshots-execute.gif?raw=true"></p>


## Demo
<p align="center"><img src="https://github.com/alph4w0lf/LokiX/blob/master/screenshots-demo.gif?raw=true"></p>

## Inner Workings
#### LokiX Back-end
- PHP Laravel Framework (Web API)
- Python (Agent Upgrade Script)
- MySQL DBMS
#### LokiX Front-end
- VueJs Framework (Template: [vue-material-dashboard@CreativeTim](https://www.creative-tim.com/product/vue-material-dashboard))
#### LokiX Agent
- C# (.NET Framework 4.5)
- Loki IOC Scanner (https://github.com/Neo23x0/Loki)



