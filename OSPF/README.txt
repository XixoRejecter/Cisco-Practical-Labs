🧠 README — Understanding and Configuring OSPF
🔷 What Is OSPF?

OSPF (Open Shortest Path First) is a dynamic routing protocol used in IP networks.
It allows routers to automatically learn routes to other networks instead of manually configuring static routes.
OSPF is a link-state routing protocol — meaning each router builds a complete map (topology) of the network and calculates the shortest path to every destination using the Dijkstra algorithm.

🔹 Why Do We Use OSPF?
Benefit	Description
Dynamic learning	Routers automatically exchange routes, no need for static configuration.
Fast convergence	When a link fails, OSPF quickly recalculates routes.
Scalability	Works efficiently in small, medium, and large networks using areas.
VLSM/CIDR support	Fully supports variable subnet masks and route summarization.
Loop prevention	Uses a reliable database (LSDB) and router IDs to avoid routing loops.

In short, OSPF helps routers stay up to date with the network without manual effort.

🔹 How OSPF Works (Simple View)

Routers establish neighbor relationships with directly connected OSPF-enabled routers.

They exchange link-state advertisements (LSAs) — information about their links and networks.

Each router builds a link-state database (LSDB) containing all LSAs in the area.

The router runs the Dijkstra algorithm to calculate the shortest path to each network.

Routes are added to the routing table.

🔹 OSPF Terminology
Term	Meaning
Router ID (RID)	A unique identifier (like a name) for the router in OSPF, usually a loopback IP or manual setting.
Area	A logical group of routers — helps scale large networks. The main area is Area 0 (Backbone area).
LSA	Link-State Advertisement — OSPF messages used to describe networks and connections.
Neighbor	Another router directly connected and running OSPF.
Adjacency	A fully established OSPF relationship between routers that can exchange LSAs.
🔹 How to Configure OSPF

You configure OSPF under the router configuration mode in Cisco IOS.

Step-by-Step Configuration
1️⃣ Enable OSPF Process
Router(config)# router ospf 1


The number 1 is the process ID (locally significant). It identifies this OSPF instance on the router.

2️⃣ Set Router ID (Optional but recommended)
Router(config-router)# router-id 1.1.1.1


This gives the router a unique OSPF identity.
If not manually set, OSPF uses the highest loopback address, or if none, the highest active IP address on an interface.

3️⃣ Identify the Networks to Advertise

Use the network command to tell OSPF which interfaces should participate and which networks to advertise.

Router(config-router)# network <network-address> <wildcard-mask> area <area-id>


Example:

Router(config-router)# network 192.168.1.0 0.0.0.255 area 0


The wildcard mask is the inverse of the subnet mask:

255.255.255.0 → 0.0.0.255

255.255.255.252 → 0.0.0.3

🧠 Tip: You must include the networks of connected interfaces that you want OSPF to:

Run on (form neighbor relationships), and

Advertise to other routers.

You do not need to write all networks in the topology — only those connected to the router.

4️⃣ (Optional) Use passive-interface

If an interface is connected to a LAN with no routers, you can stop OSPF from sending hello packets there:

Router(config-router)# passive-interface g0/1


The LAN will still be advertised, but no OSPF neighbor relationship will form on that link.

5️⃣ Verify OSPF Operation

Check neighbors:

Router# show ip ospf neighbor


→ Should show adjacent routers in FULL state.

Check routing table:

Router# show ip route ospf


→ Should display routes learned via OSPF (O next to them).

Check OSPF process info:

Router# show ip ospf

🔹 Example of a Simple OSPF Setup
RouterA(config)# router ospf 1
RouterA(config-router)# router-id 1.1.1.1
RouterA(config-router)# network 192.168.1.0 0.0.0.255 area 0
RouterA(config-router)# network 10.0.0.0 0.0.0.3 area 0


This example:

Runs OSPF process 1

Sets the router ID

Enables OSPF on two connected interfaces

Advertises the LAN and WAN networks

🔹 Common Mistakes
Problem	Cause	Solution
No OSPF neighbors	Interfaces not in same subnet, area, or OSPF not enabled	Check IPs, area numbers, and network statements
No OSPF routes in table	No adjacency formed	Verify show ip ospf neighbor
OSPF not running on an interface	Interface not included in a network command	Add correct network with wildcard
Wrong Router ID	Automatically chosen, not manually set	Configure router-id manually
✅ Summary

OSPF is a link-state routing protocol that uses areas and Router IDs.

It automatically discovers routes and provides fast convergence.

You only advertise connected networks using the network command.

Use show ip ospf neighbor and show ip route ospf to verify operation.

Would you like me to add a diagram example (with 3 routers showing OSPF adjacencies and advertised networks) into this README? It would visually explain what happens when you configure OSPF.