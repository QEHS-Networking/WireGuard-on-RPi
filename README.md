# WireGuard on RPi
WireGuard Lessons on a Raspberry Pi for encrypting a Home-based network & Cell Phone based-VPN

**Purpose**: introduction to Cyber Security (Home-based or small networks) using industry-level Linux based encryption for IP Devices within a LAN and device encryptions (VPN-like) for outside a LAN-Router
- Use a Raspberry Pi to create encryption device for router, interior-host, and exterior-device (Cell Phone) communication (i.e. monitoring cameras using IP Addresses)
- Use a Raspberry Pi to create a home-based VPN to encrypt and re-route data communication in questionable environments
- CAUTION: these lessons are meant for education purposes and not completely secure solutions

Note: this project introduces students to all concepts and ideas for <a href="http://www.nait.ca/program_home_78547.htm">NAIT's BAIST Program</a>
- NAIT Supports Secondary Teacher Education in IT Services

**Special Thanks**: <a href="https://github.com/QEHS-Networking/WireGuard-on-RPi#special-thanks">Click Here</a>

Original Resources and Access (summaries and progressions provided below), <a href="https://github.com/QEHS-Networking/WireGuard-on-RPi#original-resources-and-special-thanks-for-this-contribution">Click Here</a>

RPi Hardware Setup Summary
- Full setup, then headless
- Ensured, Putty, X11VNC, and TightVNC
- Headless is done with outside IP (not 169.254.xxx.xxx), bridged connection through Network Connections

**Progression of Steps**
- Beginnings: how this project got started, <a href="https://docs.google.com/document/d/1gRXOkD5KD_KoTx6Xuc-qOleUip3rxFemAwz1hj_S2p0/edit?ts=5ceff3dc">
one story by Mr. Carlin</a>, <a href="https://github.com/QEHS-Networking/WireGuard-on-RPi/tree/master/Beginnings%20Backup">
Click Here for a Backup Copy</a>
- Why WireGuard? How does WireGuard work? <a href="https://github.com/QEHS-Networking/WireGuard-on-RPi#why-do-we-use-wire-guard-in-mercers-kitchen">
Click Here</a>
- Hardware Setup ... If you know how to do the following ... Just do it ... Otherwise follow the links to other repositories, instructions and documents, <a href="https://github.com/QEHS-Networking/WireGuard-on-RPi#hardware-setup---initial-setup-only">
Click Here</a>
- WireGuard Installation Instructions, <a href="https://github.com/QEHS-Networking/WireGuard-on-RPi#wireguard-installation-instructions">
Click Here</a>
- DNS Redirection
  - <a href="">NoIP<a/>: email to reactivate (green button) will come every month
  - <a href="">Duck DNS</a>
- Router Port Forwarding: <a href="">Example Router Instructions</a>, other routers will be different

General Routine
- SSH: use CMD.exe or PuTTy (must know IP First)
  - pi@192.168.1.XXX (Note: must install SSH through CMD to use it)
- Start x11vnc on RPi to use GUI-based remote software
- Use GUI or CMD or PuTTy
  - PUTTy to Copy is Highlight with mouse
  - PuTTy to Paste is a RightClick
- Have a record of ...
  - Keys: key - device pairings (look up or saved from configuration on server machine)
  - IP Addresses and subnets, with device pairings
  - All ports forwarded on router (IP Address of machine, port on machine)

---

Testing that the Android Device is within LAN (WiFi Connected) or not
- Google Play Ping Apps: Ping by Lipnic (Tested), Net Ping, Ping & DNS
  - Test to make sure this works first inside network
  - Errors might be machine actively ignores pings (might be firewall too)
- Need to leave the home network (turn off WiFi and use other network like cellular data)
- Ping computer in Home Network using app and IP Address of RPi

---

Problem Solving Ports and Sockets
- Can you see me .org: type in port to see it

---

# Why do we use Wire-Guard in Mercer's Kitchen

Summary
- Able to access all computers through one port, anything with IP Address (includes IP Cameras, etc.)
- WireGuard is same program on Client or Server side, configurations are different
- WireGuard is actually very simple ... May take a few weeks the first time but afterwards will take 15 minutes to set up a new installation

WireGuard essentially works by IPv4 Forwarding

Accessing Home Network from Android Device
- Send WireGuard Packet to IP Address through Port
- Goes to RPi Server
- WireGuard on Server allows traffic through socket and encryption services
- RPi allows traffic back to router and ...
  - out of exterior port on router (i.e. WAN)
  - to other devices based on IP Address (i.e. WiFi connected or LAN-Ethernet connected)

Note about SERVER & CLIENT Vocabulary, WireGuard can be misleading
- WireGuard is installed as an entire program on two devices
- Server: actually routing all traffic from Outside Interface to multiple sockets (network range with single port, i.e. 51820)
- Client: actually sending traffic to "router" through one specific socket
- CAUTION: this is not like TightVNC Server-Viewer Relationship (i.e. example Server-Client relationship)

---

# Hardware Setup - Initial Setup Only

RPi 3 with Current OS, <a href="https://github.com/MercersKitchen/RPi-Unboxing">Click Here for unboxing Repository in Mercer's Kitchen</a>

RPi File Configuration, see Full WireGuard Installation instructions for specific configurations
- Big Idea: use NANO (RPi, Linux-based text editor)

WireGuard App: See Google Play and iTunes (others exist; only use official one)
- For Example: TunSafe

Supported apps: iOS, Android, and Linux supported only (Windows is going to be released in Beta soon)

General Routine
- SSH: use CMD.exe or PuTTy (must know IP First)
  - pi@192.168.1.XXX (Note: must install SSH through CMD to use it)
- Start x11vnc on RPi to use GUI-based remote software
- Use GUI or CMD or PuTTy
  - PUTTy to Copy is Highlight with mouse
  - PuTTy to Paste is a RightClick
- Have a record of ...
  - Keys: key - device pairings (look up or saved from configuration on server machine)
  - IP Addresses and subnets, with device pairings
  - All ports forwarded on router (IP Address of machine, port on machine)

---

Reminder for RPi: enable routing (similar to bridging on Windows between WiFi and Ethernet)

Enabling RPi IPv4 Forwarding

pi@raspberrypi:~ $ sysctl net.ipv4.ip_forward

Return: net.ipv4.ip_forward = 1

If you did that then routing on the pi is enabled so that's good.

If you get net.ipv4.ip_forward = 0, please manually edit sudo nano /etc/sysctl.conf and add net.ipv4.ip_forward = 1
- comment out `=0` line

---

# WireGuard Installation Instructions

Combining (reference and acknowledgement)
- Follow instructions <a href="https://github.com/adrianmihalko/raspberrypiwireguard">here</a> and <a href="https://www.youtube.com/watch?v=Q6pR_JEMRQA">here</a>
- Adrian's WireGuard Document to setup WireGuard on a Machine (RPi)
- Dr. ZZs YouTube Video
- These instructions include RPi autostart file

Overview of Lesson
- Quick Start Guide to installing WireGuard as a conceptual overview, <a href="https://github.com/QEHS-Networking/WireGuard-on-RPi#quick-start-guide-to-installing-wireguard-conceptual-overview">Click Here</a>
- Detailed Guide to WireGuard, <a href="https://github.com/QEHS-Networking/WireGuard-on-RPi#detailed-guide-to-wireguard">Click Here</a>

Preparation Note:
- Create a Notepad file for all keys and other information to be copied and pasted
- Easier way to verify typing of keys: type a few letters, delete them from a representation of the key being typed (or type it with someone checking)

<a href="https://www.youtube.com/watch?v=Q6pR_JEMRQA">DrZzs Home Automation Live Stream (WireGuard VPN full setup on RPi and iPhone)</a>, Sole Purpose of RPi is run WireGuard VPN
- 00:04:16 (00:04:50)- What is WireGuard. It is a VPN in small total code and more secure (no return pings). WireGuard is new standard.
- 00:15:14 (00:17:17)- Beginning of Installation, using SSH (Mr. Mercer uses full GUI with VNC, X11VNC, and TightVNC)
- 00:26:14 WireGuard for Windows
- 00:29:09 Back to setting up WireGuard
- 00:43:17 Starting WireGuard, 00:45:45 - Completion of RPi Install
- 00:44:50 Setting up clients
- 00:47:11 Setting up WireGuard on iPhone or Android
- 00:48:51 - 00:50:46 Endpoint on Clients, need Duck DNS (Dynamic Router IP) & Port for complete socket
- 01:01:00 Port Forwarding
- 01:05:00 - Competition of iOS Setup﻿
- 01:29:18 set up another client in the configuration file of the RPi, also see adrianmihalko notes, not done

## Quick Start Guide to installing WireGuard (conceptual overview)

[Teacher Specific, classroom only] Whiteboard Understanding of WireGuard

Introduction Video: https://www.wireguard.com/quickstart/
- two peers are configured at the same time
- excellent introduction
- building the .config file from commands and repositories pre-existing
- if misunderstood, this will be re-explained in detail below

## Detailed Guide to WireGuard

Go to these <a href="https://github.com/adrianmihalko/raspberrypiwireguard">Instructions</a> for specific commands and To Do List

Below are explanation of these other instructions.

#### Section 1: remember ```reboot``` updates OS to enable next steps
- Update-Upgrade-Reboot RPi OS, ensures all packages current
- Installation of Kernel Headers
  - Kernel: input-output system of the Linux operating system
  - These start basic functionality in Linux; required when compiling code (configuration) when interfacing with the kernel
  - Similar to adding a "Library" in Java, Processing-Java, Python, etc. but for C
  - ECHO a key from a server to establish a "Trust" relationship so WireGuard installation is possible from the WireGuard Repository (similar to Windows trusting Windows Update)
  - Inject the trusted key
  - Finally, install WireGuard
- With WireGuard installed, tell RPi to route traffic through itself (without this traffic doesn't flow as a security measure)
  - OS does not act like a router natively, similar to bridging in Windows between WiFi & Ethernet
  - Needs to communicate with RPi physical Ethernet port and logical WireGuard port (i.e. ```wg0 eth0```)
- Check IPv4 forwarding works as intended

#### Section 2
- Two Choice: automatic or manual
- We will use the manual configuration
- Automatic uses C Scripts to generate keys and .config files, but these programs have a shelf life

#### Section 3: creating keys, the authentication and encryption of WireGuard
- Make a searchable directory
- Navigate inside this directory
- Using WireGuard function call GenKey, create server & client public and private keys
- ```ls``` used to view directories and contents
- Use CAT to view public and private keys (NANO is also possible)

Note: these must be typed exactly

Public and Private Key relationship is unique
- public key is generated from the private key
- private key is generated from GenKey based on MAC Address, prime numbers, and WireGuard formula (educated guess for device specific private key)

Here, TightVNC or PuTTy copy-paste functions are valuable

#### Section 4
- Inside wgkeys directory, create wg0.conf (Configuration File, system configuration files read by kernel)
- Pick the IPv4 address, with subnet prefix, based on Router's DHCP Service
  - WireGuard needs to create a virtual network separate from the router's main networking schema so it can communicate
- Pick the port WireGuard will listen for (completes socket TCP/IP Socket)

Note: 192.168.XXX.XXX/24 is NAT-style home-based virtual network (internal network)
- WireGuard client authenticates through IPv4 Address and public key
- If WireGuard see client (192.168.99.2 & public key), server checks wg0.conf
- If this matches, client is authenticated and traffic passes from WireGuard Interface to Ethernet port OUT

Note: 10.0.0.X/24 is NAT-style business-based virtual network (internal network)

CAUTION
- Server Virtual Network needs larger subnet prefix to include all clients
- Client's Virtual Network subnet prefix, /32, means it must match exactly

Note: Server-Client language does not mean WireGuard is Server-Client Relationship
- Same program on both sides
- No difference between Server & Client except .conf file
- Multiple clients defined on one WireGuard instance
- This allows for multiple clients to connect to one WireGuard instance, physically defined by single router
- Server-Client language is a close resemblance

---

CAUTION: purpose of these commands is to tell the RPi to forward traffic to the proper destinations through eth0
- Commands are done within wgo.conf
- Include in Section 4 of Detailed WireGuard Instructions for Server

```
PostUp = iptables -A FORWARD -i %i -j ACCEPT; iptables -A FORWARD -o %i -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i %i -j ACCEPT; iptables -D FORWARD -o %i -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE
```

---
#### Section 5: start WireGuard with a WireGuard Function called ```wg-quick```
- Add logical interface of wg0 to "UP" (i.e. physical port is UP when lights flashing)
  - Sets configuration logical interface
  - Sets logical interface with IPv4/XX
  - Sets ICMP packet size
- Check wg is working
- If it is working, then create an auto startup script to execute WireGuard at Startup

Note: wg-quick brings up and down WireGuard Tunnel easily based on wg0.conf

CAUTION: if auto-start script is not run and there is a power failure, then RPi will not start WireGuard, leaving network inaccessible
- WireGuard service must respond for routing traffic through RPi, to access network
- Makes for easier troubleshooting when network inaccessible
- Note: unplugging the RPi from physical ports in network removes "tunnel" and ability to connect to network from the ```outside```

---

Addition to Consider

In RPi Server: `PersistentKeepalive = 25`
- In the Peer Client, last line

---

#### Section 6: Device Configuration

How do you copy and paste public and private keys to device (i.e. Android Phone)
- Method 1: email .txt of keys (CAUTION: email not secure, yet convenient)
- Method 2: print .txt to paper and cross out characters as typed (secure and painful)

**App Interface**

Install WireGuard on Clients is same as on a server (i.e. Linux or iOS devices, Windows Client is "in the works")
- WireGuard is currently most effective for mobile devices outside authenticated router WiFi

Go to Google Play Store or Appel Store

Download the Official App
- Note: although still in Beta form, WireGuard is approved by Linus Torvalds, 20190530
- Android, <a href="https://play.google.com/store/apps/details?id=com.wireguard.android&hl=en_CA">Play Store</a>
- Apple, <a href="https://itunes.apple.com/us/app/wireguard/id1441195209?mt=8">App Store</a>

Enter Interface Name, Network Name

Enter Private and Public Keys, two methods
1. Generate Private and Public Keys on RPi, copy both to device app (best practice)
2. Able to generate App Public and Private to be copied to wg0.conf in RPi

Enter (define) WireGuard Interface IPv4 Address in App
- refer to wg0.conf
- Note: this is the logical IPv4/24 address (describes split tunneling, beyond scope of this exercise)
- Alternate Example: 192.168.99.3/32 points to very specific address, not range

Listen Port is randomly generated on Client, defined on Server

Enter Addresses

Enter DNS Servers (answer what you would like to happen)
- ```8.8.8.8```: Google DNS
- ```9.9.9.9```: Quad-9 DNS
- ```1.1.1.1```: Cloud Flare DNS
- ```176.103.130.130``` and ```176.103.130.131```: Ad Guard DNS
- OR
- Pipe DNS Resolution through tunnel by providing IPv4 of router (i.e. 192.168.1.1): Router handles all DNS requests (router must be able to handle DNS Requests)

**Add Peer**
- CAUTION: this is the RPi or previously the Server (language switches depending on perspective)

Enter Public Key: RPi Public Key (Server Public Key)

No Pre-shared Key (no entry)

Enter Allowed IPv4's
- Best Practice: 0.0.0.0/0 routes all device traffic through WireGuard
- Alternate Entry deals with Split Tunneling, beyond scope of this exercise
  - Enter RPi IPv4/32 WireGuard Virtual Address (i.e. 192.168.99.1/32)
  - Enter Home Physical Network (i.e. 192.168.1.1/24)
  - Split tunneling works if some traffic is socket defined outside WireGuard by specific applications

Enter Endpoint: Public IP Address of Home Network
- This changes regularly due to DHCP of ISP Provider (i.e. Telus, Shaw, etc.)
- Therefore define friendly name URL for your Home IPv4
- Home IPv4 is tracked via DDNS Provider (i.e. No IP, Duck DNS, etc.)
  - Anytime Home IPv4 changes, DDNS Provider updates changes

Enter Persistence Keepalive: ```25```
- Allows connection to continuously communicate
- Minimizes dropouts
- Defined on both Server Side (RPi) and Client-side (mobile app)

**Additional Information**

Best Practice: delete all keys (public and private) from both server and client
- Removes sensitive data, not WireGuard function

---

# DNS Redirection (Domain Name Service)

#### NoIP

Dynamic Domain Name Server: https://www.noip.com/

Summary of Steps
  - Choose Domain Name
  - Choose ddns.net
  - Create an account
  - Confirm through email ... ready to go
  - Monthly email to ensure freemium (monthly activation)
  - [Option: turn off IP on router and add DUC on a machine, with noip.com program download to create router IP]
  - Last EMail Welcome has a list of instructions
- [Option] Duck DNS .org
- Verify registration

Machine needs to be on 24/7
- If machine gets turned off use DUC

#### Duc DNS

Used only if Router cannot be DDNS Client

<a href="https://www.duckdns.org/index.jsp">Duck DNS Home</a>
- Login with a service to save documentation
- Duck DNS will save tokens, domain names, etc.
- Able to fully delete information when not needed

Instruction set with additions that are different than the website
- NOTE: website has some explanations as what things do, these are more hand skills
- Create Domain, choose domain name, save to Notepad file for later remembering
- Choose Pi Operating System
- Enter Domain Name
- Use PuTTy to SSH to clean installation of RPi
- Run these commands, one at a time
  - `NOTE: NANO is used below but vi is listed in website, I liked nano more`
  - $ mkdir duckdns
  - $ cd duckdns
  - X~duckdns $ nano duck.sh
- Put this script into duck,sh
  - CAUTION: require the Domain Name and Token from Duck DNS, or ECHO Script from Duck DNS
  - `echo url="https://www.duckdns.org/update?domains=[DOMAIN NAME]&token=[TOKEN FROM Duck DNS]" | curl -k -o ~/duckdns/duck.log -K -`
  - Save and close the file
- Move back to parent folder, `cd ..`
- Run these commands, one at a time
  - $ chmod 700 duck.sh
  - $ crontab -e
- Open the `crontab -e` with NANO
  - Add to the bottom (comments at the top, a ReadMe)
  - `*/5 * * * * ~/duckdns/duck.sh >/dev/null 2>&1`
  - Close and Save the file
- Test the file, returns a prompt
  - $ ./duck.sh
- Test if OK or KO
  - $ cat duck.log

Configuration is finished for Duck DNS

---

# Router Port Forwarding
**Following Instructions uses 1nnov8's Home Router as an Exemplar**
- Concepts and order will be the same on other routers
- Exact configuration and options may require additional research
---

Port Forwarding will depend on router type
- Note: try to maintain table consistency between inside, outside LAN and WAN Ports
- Must be UDP (not TCP)

Example App on Apple device (Google WiFi), or log into router

Must figure out Network of Router, including subnet mask (needed for WireGuard Client Configuration)

---

Setup DDNS on Asus Black Router
- <a href="https://drive.google.com/drive/folders/11RtE_L60TWHMvi1klt4c2PXJlRSTca9d">Google DOCs File</a>
- Left Hand Picker / WAN / DDNS (TAB)
- Enable DDNS Client (yes)
- Choose NoIP.com
- Hostname (from NoIP.com): innovatelab.ddns.net
- UserName or EMail (credentials from NoIP.com): mark.mercer@epsb.ca
- Password (credential from NoIP.com): see files
- Enable Wildcard: no
- WAN IP and Hostname Verification: no

Port Forwarding
- WAN (Left Hand Picker) / Virtual Server / Port Forwarding (TAB)
- Enable port Forwarding
- Work in Port Forwarding List (Manually add port forwarding)
  - Service Name: any name that makes sense
  - Source Target (any source): leave blank
  - Port Range: [port listed in Interface from WireGuard, i.e. 51820]
- In-between Steps
  - [Must connect RPi to router, will handout DHCP IP, read from inside router's DHCP Lease List]
  - LAN / DHCP Server
  - Enable Manual Assignment: yes
  - Manually Assigned IP around DHCP List (Max 64): read IP Address or change it
    - Example: 192.168.1.59
    - This configures static IP
    - Very important this never changes or port forwarding breaks
  - Click APPLY
- Work in Port Forwarding List (Manually add port forwarding)
  - Local IP: choose device (raspberry)
  - Local Port: assigned in Interface (i.e. 51820)
  - Protocol: UDP
  - Click ADD
  - Click APPLY

---

# Original Resources and Special Thanks for this contribution
Last Accessed: 20190425 unless noted below

No Free Lunch with WiFi and Personal Data: https://www.theguardian.com/business/2019/may/28/spies-with-that-police-can-snoop-on-mcdonalds-and-westfield-wifi-customers
Accessed 20190530

Resources
1. <a href="https://www.wireguard.com/">WireGuard Website</a>

2. <a href="https://www.youtube.com/watch?v=Q6pR_JEMRQA">DrZzs Home Automation Live Stream (WireGuard VPN full setup on RPi and iPhone)</a>
   - Video has entertainment purposes ... lots of talking and interesting side notes
   - Be prepared: ```pause``` video for copying and pasting TERMINAL Configuration Lines

   Preparation Note:
   - Create a Notepad file for all keys and other information to be copied and pasted
   - Easier way to verify typing of keys: type a few letters, delete them from a representation of the key being typed (or type it with someone checking)
   <a href="https://www.youtube.com/watch?v=Q6pR_JEMRQA">DrZzs Home Automation Live Stream (WireGuard VPN full setup on RPi and iPhone)</a>, Sole Purpose of RPi is run WireGuard VPN
   - 00:04:16 (00:04:50)- What is WireGuard. It is a VPN in small total code and more secure (no return pings). WireGuard is new standard.
   - 00:15:14 (00:17:17)- Beginning of Installation, using SSH (Mr. Mercer uses full GUI with VNC, X11VNC, and TightVNC)
   - 00:26:14 WireGuard for Windows
   - 00:29:09 Back to setting up WireGuard
   - 00:43:17 Starting WireGuard, 00:45:45 - Completion of RPi Install
   - 00:44:50 Setting up clients
   - 00:47:11 Setting up WireGuard on iPhone or Android
   - 00:48:51 - 00:50:46 Endpoint on Clients, need Duck DNS (Dynamic Router IP) & Port for complete socket
   - 01:01:00 Port Forwarding
   - 01:05:00 - Competition of iOS Setup﻿
   - 01:29:18 set up another client in the configuration file of the RPi, also see adrianmihalko notes, not done

3. <a href="https://github.com/adrianmihalko/raspberrypiwireguard">Code and configuration used, from Adrian, referenced in video</a>
   - Hints and Tips are along this DOC
   - Read this closely and move slowly with the video

Extra:
   - <a href="https://p3lim.net/2018/08/27/wireguard">Setting up a WireGuard VPN Server</a>: IT Tech says there are some mistakes but pretty good

---

# Trouble Shooting

- Ensure keys are in the correct places: server and client
- Ensure port is correct (three places): server, client, and router
- Ensure the endpoint (Duck DNS) is correct (target of client)

CAUTION: in the client for ALLOWED IP's on the Client (see 01:30:20)
- if use 0.0.0.0/0 at the end of the ALLOWED IP
- then all traffic through client will go to WireGuard, not a split tunnel based on IP Address and Port
- this includes all Banking information, Google Searching, etc. to go through Home Network first (works like VPN)
- Requires basic understanding of where traffic is originating, etc.

Commands to start and stop WireGuard
```
$ wg-quick down wg0
$ wg-quick up wg0
$ wg (for status, if connected should get latest handshake)
```

---
# Special Thanks

Edmonton Public Schools IT Services for supporting Collaboration between Campus EPSB Computer Science & Networking.

Erik Carlin (EPS IT Services) for his initiative, vision, and dedication to the education of students.

The greater Raspberry Pi communication for open source and resource sharing, especially the individuals who are referenced through these lessons.

Queen Elizabeth High School and Sue Bell for a vision to support Career Pathways and a Trade, IT Services, that provides opportunity to students establishing their purpose and dignity.

---

# To Include

Diagram of How Wire Guard works as a
- VPN for Cell Phone Encryption
- Encryption for Router in home-based network application

Extra Safe - Static IPv4 Address
- Static Address on RPi AND Router's DHCP (best practice)
  - RPi: setup menu (BIOS or ```raspi-config``` or Raspberry Configuration)
- OR
- Set Router's RPi IPv4 as Static (not prefered)
  - Set RPi with static address (best practice)

Copy over all notes from Previous WireGuard Repos
- Use First: https://github.com/QEHS-Networking/Wireguard-Notes/tree/master/New%20Handout
- Backup: https://github.com/QEHS-Networking/Wireguard-Notes
- Copy all Files and Folders from: https://github.com/QEHS-Networking/Wireguard-Notes to Public README.md
- Reference https://github.com/adrianmihalko/raspberrypiwireguard as starting instructions and terminal commands
- Include SocksProxy explanation (see Erik)
- Include Erik's Google Doc Starter Story: https://docs.google.com/document/d/1gRXOkD5KD_KoTx6Xuc-qOleUip3rxFemAwz1hj_S2p0/edit?ts=5ceff3dc
- Verify RPi Unboxing: https://github.com/MercersKitchen/RPi-Unboxing
- Teaching Tip: log into Black Router and Demonstrate port-forwarding instructions & DDNS Configuration

Erik to review Public Repository

Erik to extend by creating SSH Service Video

Erik to explore SocksProxy

Future Story
- Secure traffic from inbound to outbound - much more important (Wanacry Virus)
- Use Firefox

Additions: Firewall, Untangle (see: https://www.untangle.com/, accessed 20190305)

---
