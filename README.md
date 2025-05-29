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
This workshop is split into five videos which will be broken down into 4 sections below for easier reading and organization (part 2, part 3, part 4, part 5). Part 1 is ommitted as it contained an introduction and prequisites for the workshop.

#### Part 2 (Setting up WS)
Part 2 includes: 
- WS configuration profiles
- Web traffic & default WS display
- Create a few different search filter expressions

To configure profiles: Edit at the top toolbar > Configuration Profiles > copy Default profile > rename to "Updated" or whatever you wish > OK. <br/>
Any changes made to WS will now be made to the Updated configuration profile. The Updated configuration file is located in a different location. 
<p align="center">
Configuration profiles: <br/>
<img src="https://i.imgur.com/eMATvbW.png" height="40%" width="40%" alt="pfSense Steps"/>
<br />
