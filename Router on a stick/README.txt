Router-on-a-Stick (Inter-VLAN Routing) Lab
📘 Overview
This project demonstrates Router-on-a-Stick configuration to enable inter-VLAN communication between multiple VLANs using a single physical interface on a router.
In this lab, I configured:
•	1 Router
•	1 Switch
•	6 PCs
•	3 VLANs (each VLAN has 2 PCs)
The goal was to:
1.	Create and assign VLANs on the switch

2.	Configure trunking between switch and router

3.	Create subinterfaces on the router for each VLAN

4.	Assign IP addresses and enable inter-VLAN routing

5.	Verify connectivity between hosts in different VLANs
________________________________________




🖥️ Network Topology
            +----------------+
            |     Router     |
            | G0/0           |
            +-------+--------+
                    |
                    | Trunk Link
                    |
             +------+------+
             |   Switch    |
             +-------------+
          /        |        \
         /         |         \
    VLAN 10     VLAN 20    VLAN 30
   (PC1, PC2)   (PC3, PC4) (PC5, PC6)
________________________________________
⚙️ Step 1: VLAN Configuration on Switch
Create VLANs
Switch# configure terminal
Switch(config)# vlan 10
Switch(config-vlan)# name SALES
Switch(config-vlan)# exit

Switch(config)# vlan 20
Switch(config-vlan)# name HR
Switch(config-vlan)# exit

Switch(config)# vlan 30
Switch(config-vlan)# name IT
Switch(config-vlan)# exit
Assign Ports to VLANs
Switch(config)# interface range fa0/1 - 2
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 10
Switch(config-if-range)# exit

Switch(config)# interface range fa0/3 - 4
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 20
Switch(config-if-range)# exit

Switch(config)# interface range fa0/5 - 6
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 30
Switch(config-if-range)# exit
Verify VLANs
Switch# show vlan brief
📝 Explanation:
Each pair of PCs is assigned to a specific VLAN. VLANs logically segment the network, reducing broadcast domains.
________________________________________
⚙️ Step 2: Configure Trunk Between Switch and Router
Switch(config)# interface fa0/24
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk encapsulation dot1q
Switch(config-if)# exit
📝 Explanation:
The trunk port carries traffic from multiple VLANs to the router using 802.1Q tagging. This is essential for Router-on-a-Stick to work.
________________________________________
⚙️ Step 3: Router Subinterface Configuration
Router# configure terminal
Router(config)# interface g0/0.10
Router(config-subif)# encapsulation dot1q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0
Router(config-subif)# exit

Router(config)# interface g0/0.20
Router(config-subif)# encapsulation dot1q 20
Router(config-subif)# ip address 192.168.20.1 255.255.255.0
Router(config-subif)# exit

Router(config)# interface g0/0.30
Router(config-subif)# encapsulation dot1q 30
Router(config-subif)# ip address 192.168.30.1 255.255.255.0
Router(config-subif)# exit

Router(config)# interface g0/0
Router(config-if)# no shutdown
Router(config-if)# exit
📝 Explanation:
Each subinterface acts as a gateway for its respective VLAN.
The encapsulation dot1q <vlan-id> command tags VLAN traffic appropriately.
For example, VLAN 10 hosts will use 192.168.10.1 as their default gateway.
________________________________________
⚙️ Step 4: Configure PC IP Addresses
VLAN	Device	IP Address	Subnet Mask	Default Gateway
10	PC1	192.168.10.10	255.255.255.0	192.168.10.1
10	PC2	192.168.10.11	255.255.255.0	192.168.10.1
20	PC3	192.168.20.10	255.255.255.0	192.168.20.1
20	PC4	192.168.20.11	255.255.255.0	192.168.20.1
30	PC5	192.168.30.10	255.255.255.0	192.168.30.1
30	PC6	192.168.30.11	255.255.255.0	192.168.30.1
📝 Explanation:
Assigning static IPs to PCs within their respective VLAN subnets allows routing to work correctly once the router subinterfaces are configured.
________________________________________
🧠 Step 5: Verification
1️⃣   Check Router Interfaces
Router# show ip interface brief
Expected output: All subinterfaces (G0/0.10, G0/0.20, G0/0.30) should be up/up.
2️⃣   Check VLANs and Trunk on Switch
Switch# show vlan brief
Switch# show interfaces trunk
3️⃣   Ping Test
From PC1 (VLAN 10), ping:
•	PC2 (same VLAN)
•	PC3 (different VLAN)
•	PC5 (different VLAN)
All should reply successfully if routing is correct.
________________________________________
🧾 Step 6: Save Configuration
Switch# copy running-config startup-config
Router# copy running-config startup-config
________________________________________
✅ Conclusion
This lab successfully demonstrated Router-on-a-Stick inter-VLAN routing.
By using subinterfaces and trunking, we enabled devices in different VLANs to communicate without needing multiple physical router interfaces.
Key Concepts Learned:
•	VLAN segmentation and management
•	Trunk link configuration
•	Router subinterface setup
•	Inter-VLAN communication testing
________________________________________
💻 Author
Your Name
Giorgi Mtchedlishvili
