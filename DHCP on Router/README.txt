DHCP from Router Lab

Objective:
-------------
This lab demonstrates how to configure a Cisco router as a DHCP server to dynamically assign IP addresses to PCs in a small network.

Topology:
-------------
Router0 connected to Switch0, which connects two PCs (PC0 and PC1). All devices are in the default VLAN 1.

How it works:
-------------
1. The router is configured with a DHCP pool.
2. PCs set to DHCP automatically request an IP address when they boot up.
3. The router assigns IP addresses from the pool (192.168.1.100 - 192.168.1.200) along with default gateway (192.168.1.1) and DNS server (192.168.1.1).
4. PCs can now communicate with the router and with each other using the dynamically assigned IPs.

Testing:
-------------
- On each PC, check IP assignment:
    > ipconfig
- Ping the router to verify connectivity:
    > ping 192.168.1.1
- Ping another PC to verify connectivity:
    > ping <other PC's IP>

Verification Commands on Router:
-------------
- Show DHCP bindings:
    > show ip dhcp binding
- Show DHCP pool status:
    > show ip dhcp pool

Notes:
-------------
- Switch is using default VLAN 1. No VLAN configuration is required.
- Router interface G0/1 must be up and connected to the switch.
