🧭 RIP Dynamic Routing (Beginner Level)
🧠 Overview

This lab demonstrates dynamic routing using RIP (Routing Information Protocol) between two routers.
Instead of manually adding static routes, routers automatically share and learn routes to reach other networks.

RIP is a distance-vector routing protocol that uses hop count as its metric (maximum 15 hops).
We’ll use RIP Version 2, which supports subnet masks (classless routing).

🏗️ Topology
Device	Interface	IP Address	Network	Description
R0	G0/0	192.168.1.1/24	192.168.1.0	LAN1
R0	G0/1	10.10.10.1/24	10.10.10.0	Link to R1
R1	G0/0	10.10.10.2/24	10.10.10.0	Link to R0
R1	G0/1	192.168.2.1/24	192.168.2.0	LAN2
LANs:

R0 LAN: 192.168.1.0/24

R1 LAN: 192.168.2.0/24

Link between routers: 10.10.10.0/24

🎯 Goal

Enable RIP v2 on both routers.

Each router advertises its LAN and WAN link networks.

Verify that routers automatically learn routes to the remote LAN.

⚙️ RIP Concepts

Routing Type: Distance-vector

Metric: Hop count (max 15)

Updates: Every 30 seconds

Version: RIP v2 (supports subnet masks and authentication)

Administrative Distance: 120

🔧 Configuration Summary

Each router runs:

router rip
 version 2
 no auto-summary
 network <LAN network>
 network <WAN network>


Example:

Router0 advertises 192.168.1.0 and 10.0.0.0

Router1 advertises 192.168.2.0 and 10.0.0.0

✅ Verification
On either router:
show ip route


Expected output:

R    192.168.2.0/24 [120/1] via 10.10.10.2, 00:00:12, GigabitEthernet0/1

Connectivity Test:
ping 192.168.2.10


✅ Successful replies indicate RIP routing is functioning correctly.

🧾 Summary

RIP automates route exchange between routers.

No need for static route configuration.

Ideal for small or educational networks.

Each router dynamically learns routes to other networks.