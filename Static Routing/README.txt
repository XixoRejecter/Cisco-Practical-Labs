# Static Routing Lab

## Project Goal:

This lab demonstrates how to connect multiple routers using static routes to achieve end-to-end communication between two LANs located on different routers. The setup includes three routers (R0, R1, R2) connected in series, with a PC connected to the LAN on R2.

## Network Overview:

* R0 connects to R1
* R1 connects to R2
* R2 connects to a switch and PC0 (LAN side)
* R0 also has its own LAN network

The routers use static routing, meaning routes to remote networks are manually configured rather than learned dynamically.

## How It Works:

1. Each router knows its directly connected networks by default.

   * For example, R0 knows about its own LAN (192.168.10.0/24) and its link to R1 (10.0.0.0/30).
2. Static routes are manually configured to tell routers how to reach other networks.

   * R0 learns how to reach R2’s LAN (192.168.20.0/24) via R1.
   * R2 learns how to reach R0’s LAN (192.168.10.0/24) via R1.
   * R1 has static routes pointing both ways (to R0 LAN and R2 LAN).
3. Once all routes are configured, all networks become reachable.

   * PC0 on R2’s LAN can ping R0’s LAN IPs through R1.
   * R0 and R2 can communicate across the entire network using only static routing.

## Static Routing Principles:

* **Directly Connected Networks:** A router automatically knows about networks connected to its interfaces.
* **Static Routes:** Manually added routes that define a path to a remote network using a specific next-hop IP address.
* **Next Hop:** The IP address of the next router in the path toward the destination network.
* **Advantages:** Simple to configure and very stable for small networks.
* **Disadvantages:** Not scalable — in large networks, dynamic routing protocols like OSPF or EIGRP are better suited.

## Testing:

After configuration, verify connectivity using:

* Ping from PC0 to R0’s LAN IP (192.168.10.1)
* Ping from R0 to PC0 (192.168.20.10)
* Use traceroute to confirm the path (R0 → R1 → R2)

Expected traceroute output:
10.0.0.2 → 10.0.0.6 → 192.168.20.10

## Files:

* README.txt — This document describing the setup and principles.
* config.txt — All router configuration commands for the lab.
