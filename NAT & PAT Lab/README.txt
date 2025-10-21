DNS-Only NAT/PAT Lab

Objective:
-------------
Demonstrate how a DNS server can resolve hostnames for LAN clients in a NAT/PAT network, without using a web server.

Topology:
-------------
[PC0] --- [Switch0] --- [Router0] --- [Router1 (ISP)] --- [Server0 (DNS)]
[PC1] ---/

Device Roles:
- Router0: Main router performing NAT/PAT (192.168.10.1 inside, 203.0.113.2 outside)
- Router1 (ISP): Simulated Internet router (203.0.113.1 toward Router0, 203.0.114.1 toward Server0)
- Server0: DNS server (203.0.114.10)
- PC0/PC1: LAN clients (192.168.10.10/20)

How It Works:
-------------
1. PC0/PC1 send a DNS query for www.company.local.
2. The query is routed through Router0 → Router1 → Server0.
3. Server0 resolves www.company.local → 203.0.114.10.
4. LAN clients can successfully resolve the hostname using DNS.

IP Addressing:
-------------
Router0:
  G0/0: 192.168.10.1/24 (LAN, NAT inside)
  G0/1: 203.0.113.2/24 (toward ISP, NAT outside)
Router1 (ISP):
  G0/1: 203.0.113.1/24 (toward Router0)
  G0/0: 203.0.114.1/24 (toward Server0)
Server0:
  NIC: 203.0.114.10/24, gateway 203.0.114.1
PC0:
  IP: 192.168.10.10/24, gateway 192.168.10.1, DNS: 203.0.114.10
PC1:
  IP: 192.168.10.20/24, gateway 192.168.10.1, DNS: 203.0.114.10

Testing:
-------------
- On PCs:
  > ping www.company.local
  > nslookup www.company.local
- Expected results:
  * Hostname resolves to 203.0.114.10
  * Ping succeeds

Verification:
-------------
- On Router0: `show ip nat translations` / `show ip nat statistics`
- On Server0: verify DNS record for www.company.local
