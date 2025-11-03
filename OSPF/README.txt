# OSPF Lab - R0-R1-R2

## Topology
         R0                     R1                     R2
   LAN: 192.168.1.0/24    10.0.0.0/30           LAN: 192.168.2.0/24
   G0/1: 10.0.0.1/30      10.0.0.2/30 R0-R1     G0/1: 10.0.0.6/30
                          10.0.0.5/30 R1-R2
                          10.0.0.6/30

## Objective
- Configure OSPF in Area 0 on all routers
- Advertise LANs and point-to-point links dynamically
- Verify connectivity between LANs

## Notes
- Router IDs manually set:
  - R0: 1.1.1.1
  - R1: 2.2.2.2
  - R2: 3.3.3.3
- Wildcard masks for OSPF:
  - /24 = 0.0.0.255
  - /30 = 0.0.0.3
- Verification commands:
  - `show ip ospf neighbor` → Check neighbor adjacency
  - `show ip route ospf` → Check learned OSPF routes
  - `ping <other LAN IP>` → Test end-to-end connectivity

## Troubleshooting
- If Router ID is changed, run:
  - `clear ip ospf process` to apply changes
- Make sure all interfaces are `up/up`
- Make sure all interfaces are included in OSPF `network` statements
