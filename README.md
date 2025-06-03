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

In the following examples below, we look for OS & Web browser information in unencrypted HTTP request headers. After opening provided pcap example > click on basic web filter > follow TCP stream for first HTTP request to whichever domain/URL by right clicking > Follow > TCP stream > look for user-agent line in the HTTP GET request headers. Unsure what version the browser or OS is? Look it up! <br />
##### Examples: 
Example 1: <p align="center">
Follow TCP stream: <br/>
<img src="https://i.imgur.com/xhrPmxo.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
TCP stream information: <br/>
<img src="https://i.imgur.com/3ZgmnI7.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
10_15_7 is the latest macOS Catalina version: <br/>
<img src="https://i.imgur.com/rBu6bEr.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />

Example 2 with no host name: <p align="center">
LG Electronics as the vendor ID but only "android" as the host name: <br/>
<img src="https://i.imgur.com/QqWyo8h.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
User basic web filter & follow TCP stream of first HTTP GETrequest: <br/>
<img src="https://i.imgur.com/5fOz7dG.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
Google search reveals LM0x210APM as a LG prepaid phone: <br/>
<img src="https://i.imgur.com/dNj5Prm.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />

Example 3 with no vendor ID & host name: <p align="center">
No vendor ID & host name in frame details: <br/>
<img src="https://i.imgur.com/F8j3T4K.png" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
Basic web filter > follow TCP stream of first HTTP GET request > shows Pixel 4A as the device & Chrome as the browser: <br/>
<img src="https://i.imgur.com/ePBK7ku.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />

Example 4 with little information displayed but we want to find the host name & Windows user account name. Filter by kerberos.CNameString and expand the frame details down to CNameString. Apply CNameString as a Column to find the Windows account user name. Use basic web filter to reveal their web traffic history. <br/>
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

When investigating suspicious traffic; filtering by DHCP, nbns, or Kerberos may not provide hostname details. An option is filtering by Server Message Block (SMB) traffic to look for Host Annoucements. 
<p align="center">
SMB filter: <br/>
<img src="https://i.imgur.com/XJbq1Tt.png" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
<br />

#### Part 4
