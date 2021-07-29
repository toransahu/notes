- DNS Record Types
    - A
        - The record that holds the IP address of a domain
    - CNAME
        - Forwards one domain or subdomain to another domain, does NOT provide an IP address.
    - AAAA
        - Same as “A”, but for IPv6 addresses
    - MX
        - Directs emails to an email server
    - TXT
        - Lets an admin store text notes in the record
    - NS
        - Stores the name server for a DNS entry
    - Etc
        - https://www.cloudflare.com/en-in/learning/dns/dns-records/
        - 
- NAT - Network Address Translation
    - https://www.geeksforgeeks.org/network-address-translation-nat/
    - https://www.cisco.com/c/en/us/support/docs/ip/network-address-translation-nat/26704-nat-faq-00.html
- PAT - Port Address Translation
    - This overloads NAT’s feature
    - https://www.geeksforgeeks.org/network-address-translation-nat/
- Masquerade
- (TBD) MPLS, Broadband, LTE, Satellite
- (TBD) PPPoE
    - Point-to-Point Protocol over Ethernet
    - 
- TLS
    - TLS: TLS is a security protocol that provides privacy and data integrity for Internet communications. Implementing TLS is a standard practice for building secure web apps.
        - Privacy
        - Data integrity
    - SSL vs TLS
        - In short, a better version of SSL
        - https://www.ssl2buy.com/wiki/ssl-vs-tls
    - TLS SNI: Server Name Indication, is an addition to the TLS encryption protocol that enables a client device to specify the domain name it is trying to reach in the first step of the TLS handshake, preventing common name mismatch errors.
- DSCP
    - Differentiated Services Code Point
    - Is a packet header value
    - That can be used to request (for example) high priority or best effort delivery of the traffic
    - Related
        - Devices: TBD
        - Layer: TBD
- DHCP
    - Dynamic Hosting Configuration Protocol
    - Is a NMP (N/W management protocol), helps automate the process of configuring devices on IP networks
    - Thus assigning devices IP address
        - so that IPs don't need to be manually assigned by an admin each time a device connects
    - Thus allowing them to use network service like NAT, DNS and any communication protocols based on UDP or TCP
    - DHCP is also responsible for the configuration of domain name server (DNS) and subnet masks, as well as default gateways
    - Related
        - Devices: Router/Gateway
        - OSI Layer: 2
- NAT
    - Network Address Translation
    - Is a method of remapping an IP address space into another by modifying the network address information in IP header  of packets while they are in transit across a traffic routing device
    - Means, it enables private IP networks that uses unregistered IP address to connect to internet
        - by translating the unregistered (not globally unique) IP addresses in internal network into legal address
        - before packets are forwarded to another network
    - Related
        - Devices: Router
        - Layer: TBD
- PFE
    - Packet Forwarding Engine (Juniper routers?)
    - Related
        - Devices: Router
        - Layer: TBD
- SD-WAN
    - Software-Driven Wide Area Network
    - Related
        - Devices: Router/Gateway
        - Layer: TBD
- RPM
    - Real-time Performance Monitoring (Switch?)
    - Related
        - Devices: Switch
        - Layer: TBD
- TWAMP
    - Two Way Active Measurement Protocol (Switch?)
    - Related
        - Devices: Switch
        - Layer: TBD
- QoS
    - Quality of service
    - QoE
        - Quality of experience
- AP, Router, Modem, Switch, Bridge, Hub
- Node, Hop
- Gateway, Catenet
- LAN, WLAN, WxLAN, WAN, VLAN, VxLAN
- MAC
    - Media access control
- IP
- Port
- SSID
- BSSID
- Roaming 
- Hash(), HMAC
- OSI, TCP-IP Layers/Model
- RFC
- CNA - Captive N/W Assistance / Captive Portal
- WiFi Auth Mechanism
- LE , BLE (Bluetooth Low Energy), Beacon, vBLE
- SLE (Service Level Expectations), SLA (Service Level Agreements)
- Host
- `.local` files 
    - e.g. hostname.local
- RADIUS
    - Remote Authentication Dial-In User Service
- NAS
    - Network access server
- MAC Auth
- CoA
    - Change of authorization
- RadSec
    - RADIUS security
- Traceroute, ARP, Ping, TCP ping, TCP traceroute
- SPA
    - Source protocol address
- TPA
    - target protocol address
- Connection-oriented, Connectionless protocol
- TCP
    - Transmission Control Protocol
    - Related
        - Device:
        - OSI Layer
- UDP
- ICMP
- Packet Data, Datagram, Error-Message, Segment, IP datagram, IP fragmentation
- Ethernet
- Websocket
- Control Plane
- ACL/Policy
- Rogue, Neighbor, Honeypot
    - Honeypot SSID
    - Rogue AP, Rogue Clients
    - Neighbour APs
    - https://www.mist.com/documentation/rogue-neighbor-honeypot-aps/
- Wifi spoof
- Ssid injection
    - Xss (script in ssid name)
- DFS (dynamic frequency selection)
- WiFi bandwidth channels
- FCC, CE, Other certifications
- 2.4 GHz
- 5 GHz
- 802.11ac and all other
- RRM: Radio resource management
- SLE: Service level experience
- BGP: Border Gateway Protocol 
- PPTP:  Point-to-Point Tunneling Protocol 
    - used by an Internet service provider (ISP) to enable the operation of a virtual private network (VPN) over the Internet
- L2TP: Layer Two Tunneling Protocol 
    - an extension of the PPTP
- Layer Two:
    - Devices e.g. Network interface cards, hubs, bridges, and switches
    - OSI layers: layer 2
- Layer Three??
    - Device e.g.
        - Advanced Switch
            - Combines the functionality of a switch and a router
    - OSI layers: layer 2 and layer 3
    - Ref:
        - https://documentation.meraki.com/MS/Layer_3_Switching/Layer_3_vs_Layer_2_Switching
        - http://techgenix.com/layer-3-switch/
- LLDP: Link Layer Discovery Protocol
- WPA, WEP or WPA2
- PSK
    - Pre-shared key
- multi PSK
- PMK
    - Pair-wise master key
- OKC
    - Opportunistic key caching	
- WIDS - wireless intrusion detection system 
- EAP/802.1X
- NTP, NTP config, http://www.ntp.org/
- ZTP: Zero touch provisioning 
    - is a switch feature that allows the devices to be provisioned and configured automatically, eliminating most of the manual labor involved with adding them to a network
- MDNS (multicast DNS)
- DNS
    - Domain Name System
    - Is a hierarchical and decentralized naming system
    - For computers, services or other resources connected to internet or private network 
    - Related
        - Devices: TBD
        - Layer: TBD
- DOT1X
- dBm - decibels with milliwatt (mW) reference
    - A decibel is a logarithmic unit that is a ratio of the power of the system to some reference
    - 10 dBm (1mW) is 10 times powerful than 0 dBm
    - 20 dBm (100mW) is 10 times powerful than 10 dBm
- RX (Receive) vs. TX (Transmit) 
- Ionizing vs non-ionizing radiation
- 5G vs WiFi6
    - WiFi naming convention for past and current generation tech has been simplified
        - Wi-Fi 6 means 802.11ax technology – the new generation of Wi-Fi, present in many new routers you'll buy from now on - but not many devices as yet.
        - Wi-Fi 5 means 802.11ac technology – effectively the current generation
        - Wi-Fi 4 means 802.11n technology – many people will have networking gear based on 802.11n, but it was replaced by 802.11ac in many new routers from 2013 on.
    - WiFi6 > 5G
    - OEM original equipment manufacturer
    - OUI organizationally unique identifier
        - a 24-bit number that uniquely identifies a vendor, manufacturer, or other organization
    - MAC
    - physical address
    - EUI
    - Ref:
        - https://www.intel.com/content/www/us/en/wireless-network/5g-technology/5g-vs-wifi.html
        - https://www.cisco.com/c/m/en_us/solutions/enterprise-networks/802-11ax-solution/nb-06-5-things-WiFi6-5G-infograph-cte-en.html
- Delay vs jitter vs latency
    - Latency: time to reach a packet to destination
    - Delay: time wasted/spent before sending the packet
    - Jitter: intermittent network issue/failure/package drop
- baud