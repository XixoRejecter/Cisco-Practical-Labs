# Default Route (Stub Network)

## 🎯 Goal
This lab demonstrates how a branch router (stub network) uses a **default route** 
to send all unknown traffic to an upstream ISP router.

---

## 🧱 Topology Overview

Device | Interface | IP Address | Description
-------|------------|------------|-------------
Router0 (Branch) | G0/0 | 192.168.1.1/24 | LAN side
Router0 (Branch) | G0/1 | 10.10.10.1/24 | Link to ISP
Router1 (ISP) | G0/0 | 10.10.10.2/24 | Link to Branch
Router1 (ISP) | G0/1 | 203.0.113.1/24 | Simulated Internet
PC0 | NIC | 192.168.1.10 / 255.255.255.0 / GW: 192.168.1.1 | Branch LAN client

---

## ⚙️ How It Works
- Router0 (Branch) knows only its LAN and link network.
- It uses a **default route (0.0.0.0/0)** to send all other traffic to Router1 (ISP).
- Router1 has a **static route back** to 192.168.1.0/24 so return packets reach the LAN.
- PC0 can ping ISP or Internet networks through Router0 → Router1.

---

## 🧪 Verification
1. On Router0:
