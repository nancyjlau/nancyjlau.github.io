---
title: Networks Notes
date: 2021-06-20
description: notes on studying for the CCNA (networking device types & OSI model)
tags: [Networks, CCNA]
---
## Intro

**Networks**: a group of interconnected people or things

**Computer Network**: a group/system of interconnected computers

- can consist of desktops, computers, servers, phone, security cameras, etc

**LAN (local area network)**: any network in a single area

**WAN (wide area network)**: connects several LANS together.  
- one such example is the internet

Businesses may have private WANs to connect multiple sites together.


## Networking Devices 

**Hub, Bridge, Router, Switch**

### Hub 
- layer 1 device
  - no knowledge of addresses, repeats any data it receives
- 1 collision domain
- half-duplex
  - can't send + receive data at the same time
- wastes bandwith
- hosts receive unwanted data (security riks)
- replaced by switches

### Bridges  
Segments networks into smaller sections and looks at dest., source, and MAC address.

- layer 2 device
  - can understand and learn MAC addresses
- segments LANs
- 2 collision domains
  - can send + receive data at same time
- fewer ports
- replaced by switches

### Switches
Connects devices together and can learn which ports connect to which hosts.

- layer 2 device
  - can learn MAC addresses
- full-duplex
  - can send+receive at same time
- multiple collision domains
- saves bandwith

```
            BBBB:BBBB:BBBB
                -----
               |  B  |
                -----
                  |
AAAA:AAAA:AAAA    |      CCCC:CCCC:CCCC
 -----         --------     -----        
|  B  | ----- | switch | --|  C  |
 -----         --------     -----

```

| MAC Address          | Port|
|----------------------|-----|
| AAAA:AAAA:AAAA       | 1   | 
| CCCC:CCCC:CCCC       | 3   | 
| BBBB:BBBB:BBBB       | 2   | 


### Routers
  - way out of internal network to outside world
  - routes traffic between networks
  - layer 3 device
    - can use IP address AND MAC addresses
  - fewer ports
  - highly configurable


## OSI Model

- 7 layers
- standardize communication
- same concepts as the TCP/IP model, except OSI model isn't actually used irl 

| OSI Model     |  description  |
|---------------|---------------|
| layer 7 - application  |  SMTP, FTP, Telnet | 
| layer 6 - presentation | format data, encryption| 
| layer 5 - session     | start & stop sessions| 
| layer 4 - transport    | TCP, UDP, port numbers, | 
| layer 3 - network      | IP Address, Routers| 
| layer 2 - data link    | MAC Address, switches| 
| layer 1 - physical     | cable, network interface cards, hub| 

### acronym: APSTNDP  
| All | People | Seem | To | Need | Data | Processing |  
|-----|--------|------|----|------|------| -----------|
| Application | Presentation | Session | Transport | Network | Data Link | Physical | 
### Troubleshooting Issues:  

Example: problem with network, go through all layers 
to fix  
  
#### Layer 1 (Physical)  
  - is the cable plugged in, is the network card functioning?
  - faulty cable?  

1. Check if the network cable is properly plugged in at both ends (computer/network card and switch/router).
2. Verify the network card functionality by checking if it's enabled and drivers are up to date.
3. Inspect for any physical damage or loose connections in the cables and connectors.
4. Test the network cable with a known-working cable to rule out a faulty cable.
5. Check for any potential interference from nearby electronic devices.
  
#### Layer 2 (Data)
  - maybe the switch has gone bad?  

1. Ensure that the switch is operational and powered on.
2. Check for any port-related issues on the switch, such as errors, collisions, or port shutdowns.
3. Verify that the network interface settings (speed, duplex) on both ends (computer and switch port) match and are appropriate for the network environment.
4. Try connecting to a different switch port to check if the issue is related to a specific port on the switch.
5. Inspect for any MAC address conflicts on the network.
   - look at the ARP table to see if there are duplicate MAC addresses w/ IP addresses
     - Windows: `arp -a`
     - macOS:  `arp -n`
   - use `arp-scan` to identify all active MAC addresses in local network segment for *MAC Address Discovery*
   - compare switch MAC tables
   - physical inspection if it's a small network
     - maybe devices misconfigured with same MAC address
   - Then *after*, fix the conflicting MAC address and power cycle the affected devices to clear ARP tables and MAC address caches
  
#### Layer 3 (Network)
  - is the router functioning? 
  - do i have the right IP Address?

1. Verify that the router or default gateway is functioning correctly and powered on.
2, Check the router's configuration to ensure it has the correct routing settings.
3. Verify that the computer or device has the appropriate IP address and subnet mask configuration.
4. Check for any IP address conflicts within the network.
5. Test the network connectivity by pinging the router/gateway and other devices within the same network.
  
#### Layer 4 (Transport)  
1. Check if there are any issues with the transport layer protocols (e.g., TCP, UDP).
2. Verify if the correct port numbers are being used for communication.
3. Check for any firewall or security software blocking the transport layer communication.  

#### Layer 5 (Session)
(responsible for establishing, maintaining , synchronizing, and terminating sessions between end user applications)
1. Ensure that the session establishment and management are working correctly.
2. Check if there are any issues with session-related protocols (e.g., SSL/TLS).

#### Layer 6 (Presentation)

1. Verify if the data format and encoding are compatible between devices.
2. Check if there are any issues with encryption/decryption or data compression/decompression.

#### Layer 7 (Application):

1. Investigate the specific application or service that is experiencing issues (e.g., web server, email client, file transfer application).
2. Check if the application is running correctly and if there are any known problems or bugs.

