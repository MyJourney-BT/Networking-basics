start : 20/05/2026 (dd/mm/yyyy)
# Networking Basics

Topics I am learning for Blue Team / SOC:

###  Phase 1: Networking Fundamentals (The Core)

- [ ] **OSI Model & TCP/IP Stack** (Understanding how data travels)
- [ ] **IP Addressing & Subnetting** (Mastering IPv4, CIDR, and local networks)
- [x] **MAC Address & ARP** (Layer 2 communication and its vulnerabilities)
- [ ] **DNS (Domain Name System)** (The phonebook of the internet)
- [ ] **DHCP** (How devices get IPs automatically)
- [ ] **ICMP** (Ping, Traceroute, and network diagnostics)
- [ ] **LAN / WAN Concepts**

###  Phase 2: Traffic & Packet Analysis

- [ ] **Switching & Hubs** (Flooding, CAM Tables, and Broadcast domains)
- [ ] **TCP vs UDP** (Connection-oriented vs Connectionless)
- [ ] **Common Ports** (SSH, HTTP, HTTPS, FTP, etc.)
- [ ] **HTTP / HTTPS & TLS/SSL** (Web security and encryption)
- [ ] **Wireshark Basics** (Capturing and filtering real-time traffic)
- [ ] **Packet Flow Analysis** (Tracing a packet from source to destination)

###  Phase 3: Infrastructure & Defense

- [ ] **Routing Concepts** (Static vs Dynamic routing)
- [ ] **VLANs (Virtual LANs)** (Segmenting networks for security)
- [ ] **NAT (Network Address Translation)** (Private vs Public IPs)
- [ ] **Firewalls** (Stateful vs Stateless inspection)
- [ ] **VPN (Virtual Private Network)** (Secure tunnels over the internet)

###  Phase 4: Security Operations (The Expert View)

- [ ] **MAC Flooding & Port Security** (Defending Layer 2 - *In depth*)
- [ ] **Malicious Traffic Detection** (Spotting C2 patterns and malware beacons)
- [ ] **Brute Force & Scan Analysis** (Identifying attacker recon activities)
- [ ] **IDS/IPS Basics** (Intrusion Detection/Prevention Systems)
- [ ] **Network Logs Analysis** (Reading the "footprints" of an attacker)

------------------------------------------------------------------------------------
I learned that devices in the same LAN do not need a router to communicate with each other.  
They communicate through a switch.  
Routers are used to connect different networks together.

I learned that switches can use flooding when they do not know where the destination device is located in the LAN.
Once the switch knows the destination MAC address , it can forward frames directly to the correct device.

I learned that if Device A wants to send data to Device B but only knows Device B’s IP address, it must use the ARP protocol (by sending a broadcast) to find Device B’s MAC address. 
Only then can it encapsulate the destination MAC address (Device B's MAC) along with the source MAC address and the packet into a single frame to send to the switch, which then continues the forwarding process.

1. The Vulnerability: MAC Flooding Attack
* **Mechanism:** Attackers exploit the fact that a switch's **MAC Address Table (CAM Table)** is shared and has a limited storage capacity.
* **How it works:** The attacker uses automated tools to flood a single switch port with millions of fake MAC addresses until the CAM table is completely full.
* **The Consequence:** Once the CAM table overflows, the switch fails to learn new addresses and degrades into a **Hub**. It is forced to `flood` all subsequent incoming traffic out of all ports. The attacker can then use a packet sniffer (like Wireshark) to capture sensitive data from any device in the LAN.
2. The Defense: Port Security
* **Definition:** A Layer 2 security feature on switches that restricts the number of valid MAC addresses allowed to connect to a specific port.
* **How it protects:** By setting a maximum limit (e.g., maximum 1 MAC address per port), if an attacker tries to flood the port with multiple MACs, the switch detects a violation and triggers a security action (typically **Shutdown**, which disables the port immediately). This completely neutralizes the MAC Flooding attempt.

*ARP is incredibly 'naive': It operates on a 'last response wins' basis. If two devices answer an ARP Request, the victim's computer doesn't get confused—it just blindly updates its ARP cache with whichever reply arrived last.
*The Race Condition: In an ARP Spoofing attack, the hacker's machine sends continuous, rapid ARP replies. This ensures the hacker's MAC address is the final one recorded in the victim's table, effectively overwriting the legitimate owner's info.
*The Silent Redirect: Once the victim's ARP cache is poisoned, all their traffic is routed to the hacker instead of the intended destination. The hacker can then sniff the data before forwarding it to the real target, making the attack almost invisible to the average user.


I learned that these 6 things are the main targets in a local network:
-MAC Address Table: Can be flooded to turn a smart switch into a dumb hub.
-ARP: Can be spoofed to redirect traffic because it's too trusting (Man-in-the-Middle).
-DHCP: Can be starved (DoS) or faked (Rogue DHCP) to control how users connect.
-DNS: Can be poisoned to redirect users to fake websites.
-VLAN: If not configured, an attacker can access sensitive departments from any plug.
-Default Gateway: The 'Ultimate Prize' for hackers—control the gateway, control the whole internet flow.
