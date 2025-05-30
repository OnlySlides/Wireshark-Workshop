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

#### Part 2 (WS prefences set-up)
Part 2 includes: 
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
: <br/>
<img src="" height="30%" width="30%" alt="Wireshark Workshop"/>
<br />
: <br/>
<img src="" height="40%" width="40%" alt="Wireshark Workshop"/>
<br />
