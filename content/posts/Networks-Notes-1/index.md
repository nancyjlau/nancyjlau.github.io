---
title: Networks Notes
date: 2021-06-20
description: notes on studying for the CCNA
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

## IP Address

An IP address is a logical identifier for an interface that is connected to the network. Two versions of IP are currently in use: IPv4 and IPv6

> The most common is an IPv4 address. It is a 32 bit identifier made up of four 8-bit fields called octets converted from binary to decimal numbers, separated by dots. The first part of an IP address identifies the network on which the host resides, while the second part identifies the particular host on the given network. The network number field is called the network prefix. All hosts on a given network share the same network prefix but must have a unique host number. In classful IP, the class of the address determines the boundary between the network prefix and the host number.

Subnets  
- The same goes for a subnet mask which is also represented as a number of four bytes (32 bits), ranging from 0 to 255 (0-255).  


Subnets use IP addresses in three different ways:
1. Identify the network address
2  Identify the host address
1. Identify the default gateway

{{< zoom-img src="img/subnetting.png" >}}



## LAN Topologies  
Star topology  
- expensive but scalable in nature
- prone to failure
- bigger network scale = more maintenance to keep network functional

Bus topology
- relies on a single connection (backbone cable)
- similar to leaf off of a tree
- prone to becoming slow and bottlenecked
- cost efficient 
  - cabling or dedicated networking equipment
- little redundancy in case of failures
  - single point of failure of the backbone cable  

Ring topology
- less prone to bottlenetcks
- sengs data across loop until reaching destined device
- one direction for data to travel
  - easy to troubleshoot
- not efficient to send data over

## ARP Protocol
- allows a device to associate its MAC address with an IP address on the network  

2 types of messages
1. ARP Request
2. ARP Reply

> When an ARP request is sent, a message is broadcasted to every other device found on a network by the device, asking whether or not the device's MAC address matches the requested IP address. If the device does have the requested IP address, an ARP reply is returned to the initial device to acknowledge this. The initial device will now remember this and store it within its cache (an ARP entry). 

## DHCP Protocol
 DHCP (Dynamic Host Configuration Protocol)
- Automatically assigns IP addresses 

3 types of DHCP Packets
1. DHCP Discover
2. DHCP Request
3. DHCP ACK

> When a device connects to a network, if it has not already been manually assigned an IP address, it sends out a request (DHCP Discover) to see if any DHCP servers are on the network. The DHCP server then replies back with an IP address the device could use (DHCP Offer). The device then sends a reply confirming it wants the offered IP Address (DHCP Request), and then lastly, the DHCP server sends a reply acknowledging this has been completed, and the device can start using the IP Address (DHCP ACK).

## DNS (Domain Name System)
- DNS (Domain Name System) provides a simple way for us to communicate with devices on the internet without remembering complex numbers. 

{{< zoom-img src="img/dns-hierarchy.png" >}}

- TLD (top-level domain)
1. gTLD (generic top level)
   - .com, .org, .edu
2. ccTLD (country code top level)
   - .ca, .co.uk

- second level domain
In `google.com`, `.com` is part of the TLD and `google` is part of the second level domain.  

Second level domains are limited to 63 characters and can only use a-z 0-9 and hyphens (cannot sstart or end with hyphens, or consecutive hyphens)


DNS Record Types
- A Record
  - resolve to IPv4 Addresses
- AAAA Record
  - resolve to IPv6 Addresses
- CNAME Record
  >  These records resolve to another domain name, for example, TryHackMe's online shop has the subdomain name store.tryhackme.com which returns a CNAME record shops.shopify.com. Another DNS request would then be made to shops.shopify.com to work out the IP address
- MX Record
  > These records resolve to the address of the servers that handle the email for the domain you are querying, for example an MX record response for tryhackme.com would look something like alt1.aspmx.l.google.com. These records also come with a priority flag. This tells the client in which order to try the servers, this is perfect for if the main server goes down and email needs to be sent to a backup server.
- TXT Record
  > TXT records are free text fields where any text-based data can be stored. TXT records have multiple uses, but some common ones can be to list servers that have the authority to send an email on behalf of the domain (this can help in the battle against spam and spoofed email). They can also be used to verify ownership of the domain name when signing up for third party services.
## Networking Devices 

**Hub, Bridge, Router, Switch**

### Hub 
- layer 1 device
  - no knowledge of addresses, repeats any data it receives
- 1 collision domain
- half-duplex
  - can't send + receive data at the same time
- wastes bandwith
- hosts receive unwanted data (security risk)
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

## TCP/IP model  
A model designed to standardized computer networking  
(used in the real world)  

| TCP/IP  (old) |  TCP/IP (new)|   OSI Model |
|---------------|--------------|--------------
| Appplication  | Application  | Application/Presentation/Session
| Transport     | Transport    |  Transport
| Internet      | Network      |  Network
| Link          | Data Link    |  Data Link
|               | Physical     |  Physical

Here's the OSI model again for comparison:  

| OSI Model     |  description  |
|---------------|---------------|
| layer 7 - application  |  SMTP, FTP, Telnet | 
| layer 6 - presentation | format data, encryption| 
| layer 5 - session     | start & stop sessions| 
| layer 4 - transport    | TCP, UDP, port numbers, | 
| layer 3 - network      | IP Address, Routers| 
| layer 2 - data link    | MAC Address, switches| 
| layer 1 - physical     | cable, network interface cards, hub| 

Let's look at the protocols at each layer of the TCP/IP model:

|  TCP/IP      |   Protocols |
|--------------|--------------
| Application  | HTTP, FTP, SMTP |
| Transport    |  TCP, UDP |
| Network      |  IP, Routers |
| Data Link    |  Ethernet, Switches |
| Physical     |  Cables, NIC |
 

### What happens when data is sent over?  

Encapsulation  
Layer 5 - data  
Layer 4 - (segment) TCP | data     (adds source & dest port number, seq numbers)  
Layer 3 - (packet) IP | TCP | data  (source & dest IP address)  
Layer 2 -  (frame) Ethernet | IP | TCP | Data | Ethernet  (header (mac address) and trailer (error checking))
Layer 1 - the data is physically sent  

Decapsulation  
Layer 1 -> 2 - check dest Mac address for the frame
Layer 3 -> 4 - check packet IP information
Layer 5 - transport info is read and sent to receiving application

## TCP vs UDP

TCP has ACK and sequence numbers, and a checksum to make sure all data is sent.  
 ```
          - SYN ->  
DEVICE  <- SYN-ACK -    DEVICE  
          - ACK ->  
```
Checksum confirms is data received is correct or not, if there is a mismatch then packets will be dropped.  

UDP sends data without checking, it is good for uses like video streams, online games, and VoIP. TCP is good for web browsing and email.  

### Most common port numbers:  
{{< zoom-img src="img/common-port-nums.png" >}}  

