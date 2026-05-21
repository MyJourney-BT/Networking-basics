start : 20/05/2026 (dd/mm/yyyy)
# Networking Basics

Topics I am learning for Blue Team / SOC:

- OSI Model
- TCP/IP
- IP Addressing - done
- Subnetting - done
- MAC Address - done
- ARP
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
