README.txt

VLAN Inter-VLAN Routing (Layer 3 Switch Method)

Goal:
Simulate communication between multiple VLANs using a Layer 3 switch instead of a router.

Topology:

1 × Multilayer Switch (3560)

1 × Router (for external connection or test)

4 × PCs

VLANs:

VLAN 10 → Sales → 192.168.10.0/24

VLAN 20 → HR → 192.168.20.0/24

VLAN 30 → IT → 192.168.30.0/24

Concept:
Unlike a normal Layer 2 switch, a multilayer switch can perform routing between VLANs using SVIs (Switch Virtual Interfaces).
This allows devices in different VLANs to communicate without requiring an external router.

Steps Summary:

Create VLANs and assign ports.

Create SVI interfaces with IP addresses (these act as gateways).

Enable IP routing on the multilayer switch.

Configure PCs with static IPs and gateway addresses.

Test connectivity with ping between VLANs.

Verification:

show vlan brief → confirm VLANs and port assignments

show ip interface brief → confirm SVI interfaces are up

ping <other VLAN PC> → confirm inter-VLAN communication