DHCP from Server on a Separate Network

Objective:
-------------
This lab demonstrates how to configure a DHCP server that provides IP addresses to clients located in a different LAN. 
The router acts as a DHCP relay agent, forwarding DHCP requests using the ip helper-address command.

Topology:
-------------
- Router0:
   - G0/1 (Client LAN): 192.168.10.1/24
   - G0/0 (Server LAN): 192.168.20.1/24
- Server0: 192.168.20.10/24 (DHCP Server)
- PCs: DHCP Clients connected to the 192.168.10.0/24 network
- Switch0: Client LAN switch
- Switch1: Server LAN switch

How It Works:
-------------
1. PCs in the 192.168.10.0 network broadcast a DHCPDISCOVER request.
2. Because broadcasts do not pass routers, Router0 intercepts the request on G0/1.
3. Router0 forwards the request to the DHCP server at 192.168.20.10 using:
       ip helper-address 192.168.20.10
4. The DHCP server responds with an IP address offer.
5. Router0 relays the offer back to the client.
6. The client receives its IP configuration including:
       - IP address
       - Default gateway (192.168.10.1)
       - DNS server (192.168.20.10)

Server DHCP Pool:
-------------
Network: 192.168.10.0
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.10.1
DNS Server: 192.168.20.10
Starting IP: 192.168.10.100
Max Users: 50

Testing:
-------------
- PCs should receive IPs from 192.168.10.100 - 192.168.10.150
- Ping the router (192.168.10.1)
- Ping the server (192.168.20.10)
- Ping between PCs
- Check Server0 → DHCP → Binding Table

Verification:
-------------
- PC: ipconfig
- Router: show ip interface brief
- Server: DHCP Binding Table
