# Wireshark-Workshop

## Objective
The primary focus of this workshop was to follow along with Brad to learn more of Wireshark's(WS) capabilities and how industry professionals use Wireshark as a tool to review Windows-based traffic generated from potential malware. This workshop goes over Wireshark set-up, host identification, non-malicious activity, and an introduction to Windows (Wins) malware infections. 

Source: [Brad Duncan at Palo Alto Networks Unit 42](https://unit42.paloaltonetworks.com/wireshark-workshop-videos/)

### Skills Learned
- Configure WS for personal preferences
- Follow & understand data protocol stream and its contents to identify hosts
- Understand what basic non-malicious Wins traffic looks like
- Understand what Wins malware traffic looks like

### Tools Used
- Wireshark on Linux virtual machine
- Kali on Linux virtual machine

### Takeaways
Basic query skills were learned to find flags in WS while working through the SOC analyst pathway on Hackthebox and some miscellaneous modules on TryHackMe. However, this workshop provided essential information on the capabilities WS can provide through the lens of a professional and the content that we need to understand first before diving in deeper. The content mentioned includes subjects like: vendor ID, User-Agent, verify file type in command line after export, etc. This workshop was a great introductory overview on how I can configure WS to my personal preferences, and distinguishing what may be normal vs abnormal processes. 

### Parts
This workshop is split into five videos which will be broken down into 4 sections below for easier reading and organization (part 2, part 3, part 4, part 5). Part 1 is ommitted as it contains an introduction and prequisites for the workshop.

#### Part 2 (WS prefences set-up) includes: 
- Adding custom view in a new configuration profile
- Web traffic & default WS display
- Create a few different search filter expressions

To configure profiles: Edit at the top toolbar > Configuration Profiles > copy Default profile > rename to "Updated" or whatever you wish > OK. <br/>
Any changes made to WS will now be made to the Updated configuration profile. The Updated configuration file is located in a different location. 
<p align="center">
Configuration profiles: <br/>
<img src="https://i.imgur.com/eMATvbW.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
<br />

Remove Frame number, Protocol, and Frame length. After, there should be four columns. 
<p align="center">
Example of removing frame number. Same process for protocol and frame length: <br/>
<img src="https://i.imgur.com/F7ZxpGs.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
4 columns display: <br/>
<img src="https://i.imgur.com/0LkocNG.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
<br />

To add/remove display columns: right click any column headers > column preferences > add column button at the bottom > update column title > change column type > drag column to proper location.
<p align="center">
Right click any column > column preferences: <br/>
<img src="https://i.imgur.com/MV7sRaj.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
Column preferences: <br/>
<img src="https://i.imgur.com/p1bcm17.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
Add a new column: <br/>
<img src="https://i.imgur.com/P03Sxi0.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
Update title to Port & type=destination port (unresolved: shows raw port number): <br/>
<img src="https://i.imgur.com/Dl7dbqP.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
Adding another column for unresolved source port > drag to preferred display location: <br/>
<img src="https://i.imgur.com/GsqxRtQ.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
Final column preferences: <br/>
<img src="https://i.imgur.com/Htkc83S.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
Final column display. Small nitpick here is to allign all content to the left: <br/>
<img src="https://i.imgur.com/UauHh7t.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
<br />

Optional but time display format can be edited for ease of viewing as well. View at the top toolbar > Time Display Format > UTC Year, Day of Year, and Time of Day. Select Seconds instead. 
<p align="center">
Time Display Format: <br/>
<img src="https://i.imgur.com/M79dQpl.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
Select Seconds instead of the default Automatic: <br/>
<img src="https://i.imgur.com/p6Yfh9a.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
Results - cleaner time display: <br/>
<img src="https://i.imgur.com/NLTqn0u.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
<br />

Adding additional custom columns to display domains associated with HTTP and HTTPS traffic when reviewing web traffic. Similar steps to earlier to add/remove display columns. <br />
Column preferences > Add a new column > rename to Host or Domain > Type = Custom > Fields = _http.host or tls.handshake.extensions_server_name_ > move column above Info > Apply > OK. 
<p align="center">
Add Custom column: <br/>
<img src="https://i.imgur.com/l3VLakt.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
Now see Host/Domain/URL info: <br/>
<img src="https://i.imgur.com/G3E0UTC.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
<br />

Add and save some commonly used search filter expressions as display filter buttons so there is no need to manually input the filter each time. To the right of the filter query bar > + to Add a display filter button > input name for the filter > input the specific filter query > OK. <br />
Add and save three filters: 
- Basic web filter: _(http.request or tls.handshake.type eq 1) and !(ssdp)_ is a basic search filter for web traffic that reveals HTTP URLs & HTTPS domain names, and hides SSDP traffic that is not necessary when reviewing web traffic.
- Basic+ web filter: _(http.request or tls.handshake.type eq 1 or tcp.flags eq 0x0002) and !(ssdp)_ is the basic filter and looks for TCP segments that have SYN flags because we are looking for the start or attempted start of any TCP connections.
- Basic+ web + DNS filter: _(http.request or tls.handshake.type eq 1 or tcp.flags eq 0x0002 or dns) and !(ssdp)_ is the basic+ web filter and also looks at DNS queries and responses.
<p align="center">
Add display filter: <br/>
<img src="https://i.imgur.com/apnC2Ut.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
Add basic web filter: <br/>
<img src="https://i.imgur.com/8wZXEXg.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
Add basic+ web filter: <br/>
<img src="https://i.imgur.com/BMLgDTG.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
Add basic+ web + DNS filter: <br/>
<img src="https://i.imgur.com/gi8FL36.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
Results: <br/>
<img src="https://i.imgur.com/fIjiuSB.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
<br />

Export the updated configuration file so it can be imported into WS on a different machine if needed! Edit in the top toolbar > Configuration Profiles > Export > Rename > Save
<p align="center">
Export configuration profile: <br/>
<img src="https://i.imgur.com/8V0IrB6.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
Rename configuration profile & save: <br/>
<img src="https://i.imgur.com/nT0k0D4.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
<br />
  
#### Part 3 (Host Identification) includes locating & finding: 
- Host information
- Operating System (OS) and web browser
- Windows User Account Name in Kerberos traffic from an Active Directory environment
- Other options for Windows host name

Host information: open pcap file provided on WS > click on basic web filter > first three byftes of a MAC address represents the vendor ID of the machine _but_ not always as MAC address can be changed using various methods. 
<p align="center">
Apple vendor ID example: <br/>
<img src="https://i.imgur.com/mateVg7.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
<br />

DHCP is how a host network hardware gets an IP address so if filtering by DHCP, we see an initial source IP address of 0.0.0.0 when it sends a DHCP request asking to be assigned an IP address. The DHCP server's IP address in the image below is 10.5.3.1 and issues the IP address of 10.5.3.177 with an ACK (acknowledge) message.
<p align="center">
DHCP Request & ACK: <br/>
<img src="https://i.imgur.com/5Hnd4Ic.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />

Expanding on request frame details under DHCP > we can see the requested IP address > also see the host name indicating traffic is from Apple hardware. 
<p align="center">
Frame details: <br/>
<img src="https://i.imgur.com/TxfjyhH.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />

Another option is filtering by NetBIOS name server (nbns) which can be used to dientify host names for Windows hosts & macOS hosts.
<p align="center">
Filter by nbns: <br/>
<img src="https://i.imgur.com/3RyYPZQ.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
<br />

In the following examples below, we look for OS & Web browser information in unencrypted HTTP request headers. 

##### Examples: 3.1, 3.2, 3.3, 3.4
Example 3.1: <p align="center">
Follow TCP stream: <br/>
<img src="https://i.imgur.com/xhrPmxo.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
TCP stream information: <br/>
<img src="https://i.imgur.com/3ZgmnI7.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
10_15_7 is the latest macOS Catalina version: <br/>
<img src="https://i.imgur.com/rBu6bEr.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
<br />

Example 3.2 with no host name: <p align="center">
LG Electronics as the vendor ID but only "android" as the host name: <br/>
<img src="https://i.imgur.com/QqWyo8h.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
User basic web filter & follow TCP stream of first HTTP GETrequest: <br/>
<img src="https://i.imgur.com/5fOz7dG.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
Google search reveals LM0x210APM as a LG prepaid phone: <br/>
<img src="https://i.imgur.com/dNj5Prm.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
<br />

Example 3.3 with no vendor ID & host name: <p align="center">
No vendor ID & host name in frame details: <br/>
<img src="https://i.imgur.com/F8j3T4K.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
Basic web filter > follow TCP stream of first HTTP GET request > shows Pixel 4A as the device & Chrome as the browser: <br/>
<img src="https://i.imgur.com/ePBK7ku.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
<br />

Example 3.4 has little information displayed but we want to find the host name & Windows user account name. Filter by kerberos.CNameString and expand the frame details down to CNameString. Apply CNameString as a Column to find the Windows account user name. Use basic web filter to reveal their web traffic history. <br/>
kerberos.CNameString filter is used as Kerberos traffic has TCP fragments that reveal the host name & Windows user account name. 
<p align="center">
kerberos.CNameString filter: <br/>
<img src="https://i.imgur.com/iv5yG1K.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
Apply as Column from CNameString: <br/>
<img src="https://i.imgur.com/YWAONs7.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
Scroll until a Windows account name is located: <br/>
<img src="https://i.imgur.com/A6Y5d6l.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
Basic web filter > follow TCP stream of first HTTP GET request: <br/>
<img src="https://i.imgur.com/K81995R.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
Result of TCP stream follow: <br/>
<img src="https://i.imgur.com/rbV9m1U.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
Summary of example 4. In this pcap, it looks like Windows account user rakesh.modi navigated to domain 'redhill.net.au' using Windows OS and Chrome browser. In the basic web filter screenshot, Tile-service… GET request is also HTTP but a simple search online shows that it's a default application being loaded after user sign-in. <br/>
<br/>
<br />

When investigating suspicious traffic; filtering by DHCP, nbns, or Kerberos may not provide hostname details. An option is filtering by Server Message Block (SMB) traffic to look for Host Annoucements. 
<p align="center">
SMB filter: <br/>
<img src="https://i.imgur.com/XJbq1Tt.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
<br />

#### Part 4 (non-malicious acitivy) includes:
- OS traffic
- Web browsers traffic
- Application updates
- Traffic from various protocols (Swarm, IRC, FTP, Tor, Email, SMB)
  
##### Examples: 4.1, 4.2, 4.3, 4.4, 4.5, 4.6, 4.7, 4.8, 4.9
Example 4.1: imagine investigating a possible Windows malware alert but it turns out to be a Linux OS. Open pcap > basic web filter > find port 55360 frame > follow TCP stream.
<p align="center">
Alert details: <br/>
<img src="https://i.imgur.com/IvjWqHJ.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
Port 55360 frame: <br/>
<img src="https://i.imgur.com/BMQRKDI.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
OS is Fedora Linux = resolve the alert: <br/>
<img src="https://i.imgur.com/OX8NR9Q.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
<br />

Example 4.2: pcap contains traffic from Windows 10 periodically downloading images from store-images.s-microsoft.com for Microsoft store and/or other Microsoft apps. <br />
Open pcap > basic web filter > follow TCP stream of any frame from store-images.s-microsoft.com > no user-agent line in request header is normal for this type of traffic > response headers show jpeg image as the content type. <br />
The image file can be exported as well: File > Export Objects > HTTP > Save the first image > example of the image for the Microsoft store.
<p align="center">
Follow TCP stream of store-images.s-microsoft.com host : <br/>
<img src="https://i.imgur.com/PamywHd.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
Request & Response headers: <br/>
<img src="https://i.imgur.com/lrIRQ0x.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
Export HTTP file: <br/>
<img src="https://i.imgur.com/z5VxO16.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
Save the file: <br/>
<img src="https://i.imgur.com/7zESQJf.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
Open the saved file to view image: <br/>
<img src="https://i.imgur.com/ti5g6UJ.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
<br />

Example 4.3: pcap contains traffic caused by Swarm protocol. Swarm is used to deliver Windows updates from other Windows computers (delivery optimization in system settings) using TCP port 7680 between Windows clients in the same LAN. <br/>
Open pcap > basic+ web filter > 2 TCP SYN segments represent the start of 2 TCP streams > follow first frame's TCP stream > not much data but Swarm protocol is stated in the traffic > comes from both sender and receiver. 
<p align="center">
TCP SYN frame: <br/>
<img src="https://i.imgur.com/Yc9AVGz.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
TCP stream information: <br/>
<img src="https://i.imgur.com/CUB8laO.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
<br />

Example 4.4: pcap contains traffic caused by Chrome and Edge (based on Chromium). Chrome & Edge send DNS queries for random text string queries representing non-existent domains. This is how the browsers ensure the internet service provider is not redirecting any traffic for non-existent domains. The non-existent domain queries should not resolve which is why there are repeats in the pcap; if there is a response, the response should be NXDOMAIN. <br/>
Open pcap > filter by "dns" > notice 3 DNS queries to random string of letters ending in localdomain > filter specifically by "dns.qry.name contains localdomain" > filter by "nbns". <br/>
NBNS traffic is seen due to Windows trying the same name query over NBNS if DNS query does not resolve or get a response from a DNS server.
<p align="center">
Filter by "dns": <br/>
<img src="https://i.imgur.com/Jlevn2X.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
Filter by "dns.qry.name contains localdomain": <br/>
<img src="https://i.imgur.com/3I9s9pl.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
Filter by "nbns": <br/>
<img src="https://i.imgur.com/K0Y7TOb.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
<br />

Example 4.5: pcap contains traffic caused by Chrome and Edge udpates to the browser. Updates to either browser generates HTTP traffic to domains ending in .gvt1.com to update the browser. <br />
Open pcap > basic web filter.
<p align="center">
Basic web filter: <br/>
<img src="https://i.imgur.com/9nfBII4.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
<br />

Example 4.6: pcap contains traffic generated by using FileZilla on a Windows 10 host. Traffic to 193.104.215.67 over TCP port 21 is seen. TCP port 21 is the FTP control channel; TCP ports 21637 & 50926 is the FTP data channel. <br />
Using our basic+ web + DNS filter, we will follow multiple TCP streams in this example: the 1st SYN segment to TCP port 21, the 1st SYN segment with destination port of 21637, the 2nd SYN segment going to TCP port 21, the SYN segment going to TCP port 50936.
<p align="center">
Basic + DNS filter > follow TCP stream of 3rd frame (49683 -> 21): <br/>
<img src="https://i.imgur.com/atsqAYy.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
TCP stream displays Anonymous user (logging in) & LIST which lists the directory of the FTP server: <br/>
<img src="https://i.imgur.com/Igq6AlW.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
TCP stream of 4th frame (destination port of 21637) displays a directory list from the FTP server: <br/>
<img src="https://i.imgur.com/uivjFe4.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
TCP stream of 5th frame (2nd SYN segment going to port 21) displays user retrieving a file named 'licenses.txt': <br/>
<img src="https://i.imgur.com/2qtUBSr.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
TCP stream of 6th frame (SYN segment going to port 50926) displays content of license.txt file: <br/>
<img src="https://i.imgur.com/Z7zKTv0.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
  
_ftp.request.command or ftp-data_ command can be used to see the flow of events.
<p align="center">
Flow of events: <br/>
<img src="https://i.imgur.com/5vwQ5B9.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
<br />

Example 4.7: pcap contains traffic generated by gmail using thunderbird email client on a Windows 10 host. <br/> 
Open pcap > basic+ web + DNS filter > two DNS queries for imap.gmail & smtp.gmail.com > both traffic are encrypted so following TCP stream displays nothing.  
<p align="center">
Basic+ web + DNS filter > follow TCP stream of first imap.gmail.com frame: <br/>
<img src="https://i.imgur.com/kXQI6BG.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
TCP stream encrypted contents: <br/>
<img src="https://i.imgur.com/RVqirGQ.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
<br />

Example 4.8: pcap contains traffic generated by an unsecure email using Thunderbird on a Windows 10 host. <br/> 
Open pcap > basic+ web + DNS filter > notice two SYN segments over port 110 (POP traffic) > also notice some traffic to port 587 (SMTP traffic) > SMTP traffic is encrypted after connecting to the mail server > filter by SMTP > commands to connect to mail server before a TLS encrypted pipeline is established > follow TCP stream of any SMTP frame > see SMTP traffic but no SMTP data. <br/> 
Back to basic+ web + DNS filter > follow TCP stream of first frame going to port 110 > notice plain login base64 string representing non-encrypted login data > copy the base64 string and decrypt > decrypted string states email address and password > back to TCP stream of pop traffic > email content can be seen in plaintext. 
<p align="center">
Basic+ web + DNS filter > two SYN segments over port 110 & some traffic to port 587 : <br/>
<img src="https://i.imgur.com/BsgrWM8.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
Filter by SMTP & follow TCP stream of any SMTP frame: <br/>
<img src="https://i.imgur.com/D13iR02.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
SMTP TCP stream displays traffic but no data: <br/>
<img src="https://i.imgur.com/TxInUO2.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
Basic+ web + DNS filter > follow TCP stream of either port 110 traffic: <br/>
<img src="https://i.imgur.com/pA00BjP.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
AUTH PLAIN=no information is encrypted > string is base64 binary: <br/>
<img src="https://i.imgur.com/uS21Gnk.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
Copy & paste base64 string into decoder: <br/>
<img src="https://i.imgur.com/HdRCTHS.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
TCP stream contents disaplys email content in plain text: <br/>
<img src="https://i.imgur.com/Q2wXh9z.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
<br/>

Example 4.9: pcap contains traffic recorded from an Active Directory (AD) environment with a fake domain name. In the environment, a Windows client's Z: drive is mapped to a shared folder on the Domain Controller (DC). Someone dragged a file named 2021-calendar-blank.xlsx from the Z: drive to the desktop on the Windows client. <br/>
Open pcap > export SMB objects: File > Export Object > SMB > select the file that show 100% in the content type > save the SMB export. <br/>
After exporting, WS automatically directs to the frame (Read Reponse) that was exported. Follow TCP stream > no meaningful information so ignore the ascii text and scroll up the data stream to look in Info column details > verify the file type in Kali terminal. 
<p align="center">
Export SMB objects: <br/>
<img src="https://i.imgur.com/6lrvm7C.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
Select the correct object & Save: <br/>
<img src="https://i.imgur.com/ZeFNUZ1.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
Auto directed to the frame that we exported: <br/>
<img src="https://i.imgur.com/9xy2RQu.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
TCP stream meaningless information: <br/>
<img src="https://i.imgur.com/Yr5DvPE.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
File request & response earlier in the data stream: <br/>
<img src="https://i.imgur.com/a1Cx0og.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
Locate exported file: <br/>
<img src="https://i.imgur.com/QRGkAGl.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
Kali does not have excel so verify file type via Terminal: <br/>
<img src="https://i.imgur.com/1BAiHxA.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
<br />

#### Part 5 (malicious acitivy) includes:
- Brief overview of Mass Distribution (Commodity) Malware
- Malware -> malicious HTTP traffic (generally easy to detect)
- Malware -> malicious HTTPS/SSL/TLS traffic
- Malware -> Malicious TCP traffic

There are two common types of delivery for Windows-based malware: files/links sent through email _or_ sent through (malicious) web traffic such as ads or compromised websites. 
- Typically, a Windows executable is stored within an archive file attached to an email. This is easy for email filtering to catch. <br /> How it works: Email has an attachment within -> ZIP attached archive -> extracted executable malware. Windows by default hide file extensions so victims may not see the .exe for the extracted file name. <br /> Links sent through email are more complicated but involves enabling macros on a malicious word/excel document. 
<p align="center">
Example: user may only see the Adobe file ending in pdf: <br/>
<img src="https://i.imgur.com/XvtFH3n.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
  
- Without using emails, malware can be distributed via malicious web ads or traffic. <br /> Via malicious web ads: bad actors purchase/create malicious web ads that may be posted on legitmate websites generating traffic to unwanted or malicious URLs/files. <br /> Via web ads or traffic: bad actors compromise legitimate websites by injecting code into the web pages generating traffic to unwanted or malicious URLs/files.

An example of malicious HTTP, HTTPS/SSL/TLS, and TCP traffic will be displayed below.

##### Examples: 5.1, 5.2, 5.3
Example 5.1: pcap contains post-infection unencrypted traffic caused by Formbook malware. Formbook is a messy/noisy type of malware that generate alot of HTTP GET & POST requests. Any form of Formbook will cause the same patterns in GET & POST requests; note that other Formbooks will have different patterns. <br /> Malware was delivered as an email with an attachment -> attached ZIP archive -> extracted malware. <br /> 

Open pcap > basic web filter > scroll down to see more HTTP requests > this Formbook sample has the first four characters as e8bw > follow TCP stream of any HTTP GET request > minimal information in the HTTP request headers indicates likely malicious activity > new search filter show the HTTP responses to the GET requests > basic + DNS filter > find indicators of some domains that were contacted by Formbook malware that did not resolve.
<p align="center">
e8bw Formbook pattern for any domain it's going to: <br/>
<img src="https://i.imgur.com/G2mf1Ww.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
Follow TCP stream of any initial HTTP GET request: <br/>
<img src="https://i.imgur.com/PF0Iiht.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
Minimal HTTP request headers information is likely malicious activity: <br/>
<img src="https://i.imgur.com/WODp8DV.png" height="30%" width="30%" alt="Wireshark Workshop"/> 
<br />
Edit basic web query to "(http.request or http.response or tls.handshake.type eq 1) and !(ssdp)" to view HTTP responses: <br/>
<img src="https://i.imgur.com/RBjlyk0.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
Follow TCP stream of a GET request that has a 200 OK response: <br/>
<img src="https://i.imgur.com/eZrXYIb.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
Similar minimal HTTP request headers: <br/>
<img src="https://i.imgur.com/ddeP0xG.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
Basic+ web + DNS filter & scroll around > notice some domains contacted by Formbook but they did not resolve: <br/>
<img src="https://i.imgur.com/WXS5AW8.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
<br />

Example 5.2: pcap contains post-infection HTTPS traffic caused by a Dridex malware. <br />
Malware was sent through email with an excel attachment or a link to download an excel file that enabled macros resulting in HTTPS traffic to retrieve a Dridex DLL. The DLL is used to infect the vulnerable Windows host with Dridex malware. <br/>

Open pcap > basic web filter > lots of Microsoft related traffic > scrolling around, notice some encrypted traffic to TCP port 443 with no associated domain which is unusual, and to port 7443 which is not a standard port for web traffic > notice there is one non-Microsoft related domain > Follow TCP stream of non-Microsoft related domain frame > Google search domain in quotation marks to not directly enter a possible malicious domain > check domain at https://urlhaus.abuse.ch/ (platform for sharing malicious URLs that spread malware) > Click on the result to get more information > Malicious DLL's downloaded on Mar 10 & 11, 2021 that were submitted to Virustotal. <br/>
<p align="center">
Traffic to ports 7443 & 443 with no domains: <br/>
<img src="https://i.imgur.com/Neib2F8.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br/>
1 non-Microsoft related domain & follow TCP stream: <br/>
<img src="https://i.imgur.com/PcEFME9.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
TCP stream; information shows that it's using Let's Encrypt certificate (not inherently malicious): <br/>
<img src="" height="30%" width="30%" alt="Wireshark Workshop"/>
<br/>
No results when Google searched the domain: <br/>
<img src="https://i.imgur.com/Vwcflj3.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
Domain search results in URLhaus prompted a report from March 10, 2021: <br/>
<img src="https://i.imgur.com/nzEfkhx.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br/>
URLhaus more information: <br/>
<img src="https://i.imgur.com/Eczo3Qn.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
Malicious DLL downloads: <br/>
<img src="https://i.imgur.com/8CFmvbg.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br/>

Cross reference the time from URLhaus with the pcap frame > circumstancial evidence that the HTTPS traffic returned a DLL for Dridex >
<p align="center">
Date of the traffic to domain in question: <br/>
<img src="https://i.imgur.com/Btpn7x9.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
: <br/>
<img src="" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
: <br/>
<img src="" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
: <br/>
<img src="" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
: <br/>
<img src="" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
