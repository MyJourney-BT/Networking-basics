start : 20/05/2026 (dd/mm/yyyy)
# Networking Basics

Topics I am learning for Blue Team / SOC:

- OSI Model
- TCP/IP
- IP Addressing - done
- Subnetting - done
- MAC Address - done
- ARP - done, The protocol used to discover the MAC address of a device when only its IP address is known.
- LAN / WAN 
- NAT
- DNS
- DHCP
- ICMP
- TCP
- UDP
- Ports
- HTTP / HTTPS
- TLS / SSL
- Routing - done
- Switching - done
- VLAN
- Firewalls
- VPN
- Packet Analysis
- Wireshark
- Network Logs
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
