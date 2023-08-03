---
title: Networks Notes (Part 1)
date: 2021-06-20
description: notes on studying for the CCNA
tags: [Networks, CCNA]
---

# Networks Notes Part 1

## Intro

Networks: a group of interconnected people or things

Computer Network: a group/system of interconnected computers

- can consist of desktops, computers, servers, phone, security cameras, etc

LAN (local area network): any net work in a single area

WAN (wide area network): connects several LANS together. one such example is the internet

Businesses may have private WANs to connect multiple sites together.


## Networking Devices 

Hub, Bridge, Router, Switch

**Hub**  
- layer 1 device
  - no knowledge of addresses, repeats any data it receives
- 1 collision domain
- half-duplex
  - can't send + receive data at the same time
- wastes bandwith
- hosts receive unwanted data (security riks)
- replaced by switches

**Bridges**  
Segments networks into smaller sections and looks at dest., source, and MAC address.

- layer 2 device
  - can understand and learn MAC addresses
- segments LANs
- 2 collision domains
  - can send + receive data at same time
- fewer ports
- replaced by switches

**Switches**
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


**Routers**
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
| layer 5  - session     | start & stop sessions| 
| layer 4 - transport    | TCP, UDP, port numbers, | 
| layer 3 - network      | IP Address, Routers| 
| layer 2 - data link    | MAC Address, switches| 
| layer 1 - physical     | cable, network interface cards, hub| 