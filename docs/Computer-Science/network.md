# Network

<h3>Table of Contents</h3>

[TOC]

## History

18th century: age of mechanical systems - indutries
19th century: age of steam engine
20th century: age of information + telephone networks + radios, tv, computer, satellite

earlier - a centralized computer - a big computer ina room for an org
nowadays - many distributed computers, in large quantity

with rise - need more robust, sophisticated system to monitor each part/layer/unit of the network end to end.

large number of separate computers able to exchange info i.e. interconnected == **Computer Network**

**focus**: design & organization of this network

internet/www != computer network

**internet** == collection of computer networks

**www** == **distributed system** running on top of internet

distributed system == computer network **?**

Differences
- distributed system
    - a collection of independent computers appears to its users as a **single coherent system**
    - has a single model, paradigm
        - responsible for implementing these models -> **middleware**
    - built on top of a network
    - softwares gives it a high degree of cohesiveness and transparency
    
    - e.g. 
        - www: everything looks like a document, a **Web Page**

- computer network
    - coherence, model, software are absent
    - user are exposed to the actual machines

The main differentiator is software or operating system. But no hardware.

Middleware: software that acts as a bridge between an operating system or database and applications, especially on a network.


## Basics

- Topologies
	- Bus
	- Star
	- Ring
	- Mesh
- Network Area Types
	- PAN
	- LAN
	- CAN
	- WAN
	- MAN
	- GAN
- XXX
	- MoDem
	- Repeater
		- Amplifier?
- Network Equipments/Devices
	- Hub
		- 1
			- all data to all ports
	- Bridge
		- 2
			- Remember which MAC <-> Port
	- Switch
		- similar as Bride, but newer
		- 2
			- MAC addr. table in memory
		- 3 (optional support)
			- Routing table
		- VLANs
	- Router
		- 3
			- Routing table
			- IP
	- Wireless Access Point (WAP)
		- Similar to Router, but wireless
		- Modes
			- Ad-hoc
			- Enterprise
		- Common Settings
			- SSID
			- SSID Broadcast
			- Authentication methods
				- WEP (Deprecated)
				- WPA2 PSK (WiFi Protected Access)
				- WPA2 Enterprise (RADIUS)
					- RADIUS: Central Auth Server
			- MAC Filtering
- Network Interface Card (NIC)
- NIC Types


## Network Usages

- resource sharing (more general)
- business applications
    - client-server model
    - communication / e-mail
    - e-commerce
- home aaplications
    - internet
    - remote information
    - p2p - phone, instant msg-ing
    - entertainment
    - e-com
    - fin
- mobile / wireless

## todos
- wap1.0
- wap2.0
    

# Basic Story
- Connect WiFi in laptop to your modem
- 2 ARP will happen
    - Will follow DORA process
        - Discovery: client mac will 

# Protocols

### Why
Given the importance of protocols to the Internet, it’s important that everyone
agree on what each and every protocol does, so that people can create systems and
products that interoperate. This is where standards come into play. Internet stan-
dards are developed by the Internet Engineering Task Force (IETF)[IETF 2012].
The IETF standards documents are called requests for comments (RFCs). RFCs
started out as general requests for comments (hence the name) to resolve network
and protocol design problems that faced the precursor to the Internet
RFCs tend to be quite technical and detailed

## TCP (Transmission Control Protocol)
## IP (Internet Protocol)
## UDP

https://www.smashingmagazine.com/2017/06/guide-switching-http-https/

## ICMP
(Internet Control Message Protocol)
- https://erg.abdn.ac.uk/users/gorry/eg3567/inet-pages/icmp.html
- https://cse.sc.edu/~wyxu/515Fall08/slides/IPRoutingtrace.pdf

### Why?
Because IP wasn't designed to be absolutely reliable & it doesn't have an inbuilt mechanism for sending control(errors & query) messages. ICMP comes in picture: 
- to provide feedback to the source IP address by network devices like routers (and may be switch, hub..)
    - that a router/service/host can't be reached for packet (datagram) delivery
- to answer queries raised by `ping` & `traceroute` tools 

<img src="https://erg.abdn.ac.uk/users/gorry/eg3567/images/icmp-gen.gif"/>

### What?
- ICMP is a supporting protocol
- ICMP is not a transport protocol
- ICMP is typlically not used to exchange data between systems (except in case of diagnostic tools ^)
- ICMP sits in N/W layer of OSI along with IP
    - and **hence port doesn't come in picture here**
    - ports are only used for protocols which work at the transport layer and above
- ICMP send multiple types of messages:
    - ping (echo)
    - ping reply (echo reply)
    - destination unreachable etc..
- ICMP structure
    - ICMP Header (8 bytes)
        - ICMP type
        - ICMP code (sub-type)
        - Chechsum
        - Extra content (of 4 bytes)  based on type & code
    - ICMP message (variable, min 28 bytes)
        - entire IP Header from IP datagram that resulted in error (min 20 bytes, variable)
        - atleast (first) 8 bytes of data from IP datagram that resulted in error

<img src="https://www.ionos.com/digitalguide/fileadmin/DigitalGuide/Screenshots/EN-ICMP.png"   style="align: middle;"> <center>ICMP Header Structure</center></img>

### How?
- ICMP messages are encapsulated in an IP datagrams and transmitted along with them to the transport layer
    - protocol in IP datagrams are set to ICMP
        - so that receiving end can interprete it using ICMP client
    - source address is set to the IP address of the device that generated the datagram (& ICMP message)
    - destination address is set to the source address mentioned in the packet (datagram) that resulted in error (i.e. of which delivery failed)
- Structure of IP datagram having ICMP encapsulated within it
    - IP header (20 bytes)
        - IP Protocol=ICMP
    - IP data
        - ICMP message 
            - ICMP header (1+1+2+4 bytes)
            - ICMP data (min 28 bytes, variable)

<img src="http://www.tcpipguide.com/free/diagrams/ipformat.png"> <center>IP Datagram Structure</center></img>
    
    

## HTTP, HTTPS

## TLS, SSL


## WebSocket
## SMTP
## ARP (Address Resolution Protocol)

# OSI Model
(Open Systems Interconnection)

- https://www.webopedia.com/quick_ref/OSI_Layers.asp

## Intro
- Open Systems Interconnection Model
- a conceptual model
    - characterize & standarize the communication function of telecommunication/ compututing systems
    - without any knowledge of its internal structure & technology
- partitioned in abstraction layers
- a layer serves the layer above it

## Application Layer

- User apps, Network services

### Protocols
- HTTP, HTTPS, SMTP, FTP

## Presentation Layer

- Encryption, charsets

### Protocols
- SSL, TLS, JPEG, MPEG

## Session Layer

- Setup, maintain, tear-down sessions

### Protocols
- NFS, SQL, RPC, Netbios

## Transport Layer

- Datagram delivery (TCP/UDP), port number

### Protocols
- TCP, UDP

## Network Layer

- Routing, Software adrresses (IP)

### Protocols
- IP, ICMP, ARP, RARP, IGMP

## Data Link Layer

- Media access, Hardware addresses (MAC)

### Protocols
- ARP, HDLC, PPP

## Physical Layer

- Cable, connectors, electrical specs

### Protocols
- no protocols at this layer

<img src="https://s3.amazonaws.com/hs-wordpress/wp-content/uploads/2017/12/12223329/433_061.gif"/>

# TCP/IP Model
- http://what-when-how.com/data-communications-and-networking/network-and-transport-layers-data-communications-and-networking/
- https://www.hardwaresecrets.com/how-tcp-ip-protocol-works-part-1/6/

## Application Layer
### Protocols
- HTTP, HTTPS, SMTP, FTP, JPEG, MPEG, NFS, SQL, RPC

## Transport Layer
### Protocols
- TCP, UDP

## Internet Layer
### Protocols
- TCP, UDP

## Network Interface/Access Layer (Link Layer)
### Protocols
- IP, ICMP, ARP, RARP, IGMP

# Ethernet 

Note: TCP/IP is a set of protocols that deals with layers 3 to 7 from the OSI reference model, while Ethernet is a set of protocols that deals with layers 1 and 2 from the OSI reference model


# TODOs
Packets
Packet Switch
Internet API
Internet Service
Distributed App
