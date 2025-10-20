DHCP from Server Lab - Router G0/1: 192.168.1.1

Objective:
-------------
This lab demonstrates how a dedicated server can provide DHCP addresses to PCs in a small network.

Topology:
-------------
- Router0: G0/1 = 192.168.1.1/24 (default gateway)
- Switch0: Connects PCs and server
- Server0: 192.168.1.10/24, DHCP enabled
- PCs: Receive dynamic IPs from the server

How it works:
-------------
1. Server0 is configured with a DHCP pool: 192.168.1.100 - 192.168.1.150
2. PCs request IPs when they boot up via DHCP.
3. Server0 assigns IP addresses, default gateway (router), and DNS server.
4. Router only acts as a gateway; it does not assign IPs.

Testing:
-------------
- PCs should receive IPs in the range 192.168.1.100 - 192.168.1.150
- Test connectivity:
    > ping 192.168.1.1   ! Router
    > ping 192.168.1.10  ! Server
    > ping other PCs

Verification:
-------------
- Server0 → DHCP → Binding Table shows assigned IPs
- PC → ipconfig shows assigned IP, gateway, and DNS
