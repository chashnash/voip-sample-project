# VoIP-sample-project
This is the sample project to show an internal call case in kamailio-Asterisk setup.


# Project description: 
This private sample project is intended to show the Kamailio-Asterisk integration configuration and to make a simple test call in a local private network. 
This project aims to showcase my proficiency with open-source VoIP servers in Linux (eg: Kamailio & Asterisk), VoIP Infra & Topology, SIP messages and tools/traces like tcpdump, wireshark, logs, sngrep etc.
If there is an opportunity for an Interview, I am prepared to show a live demo.

# Topology & Environment:
The Asterisk and Kamailio servers are installed on the same Debain Linux. The Debian is setup on on-premise Virtual Machine. 
 ![image](https://github.com/chashnash/voip-sample-project/assets/143314204/0d6d52f1-b47d-4be2-818c-49a5b6672574)

The Asterisk acts as PBX to handle the telephony services and calls.
Two users user1 and user2 are registered in Asterisk,  PJSIP.conf is configured to listen at port 5070. (The pjsip and extensions.conf file are available in the files)
Kamailio acts as SIP proxy, and it listens for UDP traffic on port 5060. 
All the traffic coming to Kamailio will be routed to Asterisk via port 5070. The routing logic configuration can be found in kamailio.cfg 


# Versions:
esxi 8.0 <br>
Debian 10 buster<br>
Kamailio 5.6.5<br>
Asterisk 18.20.0<br>
Microsip and 3CX Softphones on windows10<br>

# Scenario and sample case:

<ins>User registration:</ins> <br>
When a user tries to register at 172.17.0.52: 5060, the request reaches first to Kamailio, then the traffic is forwarded to Asterisk via port 5070. 
sngrep output of Call flow for User-1 registration is shown below.

![image](https://github.com/chashnash/voip-sample-project/assets/143314204/3627aae1-373e-4c75-b2f2-397bf65a9f4b)

<ins>Call scenario:</ins>

User-1 makes a call to User-2 by dialing the extension 1002. User 1 sends INVITE message to Kamailio SIP  proxy server. As per the routing logic configured in kamailio.cfg , the INVITE header is forwarded to an Asterisk via port 5070. As Kamailio is the SIP proxy server, it sends 100 trying to the User-1 and the further SIP messages are handled among User, Kamailio and Asterisk. Please find the attached Wireshark traces in the files. <br>
Trace from Kamailio server:  call-kamailio.pcap <br>
Trace from softphone: call-clients.pcapng

