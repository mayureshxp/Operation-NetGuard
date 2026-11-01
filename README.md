Operation NetGuard

Enterprise Network Security Using VLANs and Extended ACLs | Cisco Packet Tracer

1. Project Overview

Operation NetGuard is an enterprise-style network security simulation developed using Cisco Packet Tracer.

The project implements network segmentation using separate VLANs for HR, IT and SERVER departments. Router-on-a-Stick configuration enables inter-VLAN routing, while an extended Access Control List (ACL) enforces department-based access restrictions.

The primary security objective is to block IT department access to the server network while allowing HR users to communicate with the server.

2. Network Topology

The network consists of:

Device| Description
R1_HQ| Main router
SW1_HQ| Main network switch
HR_PC_1| HR workstation
HR_PC_2| HR workstation
IT_PC| IT workstation
SRV1| Server

3. VLAN and IP Addressing

VLAN| Department| Network| Default Gateway
10| HR| 192.168.10.0/24| 192.168.10.1
20| IT| 192.168.20.0/24| 192.168.20.1
30| SERVER| 192.168.30.0/24| 192.168.30.1

End-device IP addressing:

Device| IP Address
HR_PC_1| 192.168.10.10
HR_PC_2| 192.168.10.11
IT_PC| 192.168.20.10
SRV1| 192.168.30.10

4. Router Configuration — Router-on-a-Stick

Three subinterfaces were configured on "GigabitEthernet0/0":

- "Gi0/0.10" — HR gateway
- "Gi0/0.20" — IT gateway
- "Gi0/0.30" — SERVER gateway

IEEE 802.1Q encapsulation was configured to support VLAN tagging and inter-VLAN routing.

Verification command:

show ip interface brief

All three router subinterfaces were verified as operational.

5. Network Security — Extended ACL

A named extended ACL called "NETGUARD_IT_POLICY" was created to control communication between departments.

Deny rule:

deny ip 192.168.20.0 0.0.0.255 192.168.30.0 0.0.0.255

Permit rule:

permit ip any any

The ACL was applied inbound on "GigabitEthernet0/0.20".

Security policy:

- IT department traffic destined for the SERVER network is denied.
- Other traffic is permitted by the configured permit rule.
- HR users retain access to the server.

6. Testing and Results

The following connectivity and security tests were performed:

Test| Result
Router → HR_PC_1| Successful
Router → IT_PC| Successful
Router → SRV1| Successful
HR_PC_1 → IT_PC| 0% packet loss
IT_PC → SRV1| Blocked
HR_PC_1 → SRV1| 0% packet loss
ACL deny counter| 4 matches

The test results confirmed that the configured ACL successfully blocked IT-to-server communication while preserving HR-to-server connectivity.

7. Skills Practised

- VLAN configuration and network segmentation
- IPv4 addressing and default gateways
- Router-on-a-Stick inter-VLAN routing
- IEEE 802.1Q encapsulation
- Extended ACL configuration
- Department-based access control
- Network connectivity testing
- ACL verification and troubleshooting
- Cisco IOS configuration management

8. Configuration Saving

The router configuration was saved using:

copy running-config startup-config

The router returned the "[OK]" confirmation.

The Packet Tracer simulation was saved as:

"Operation_NetGuard.pkt"

9. Repository Structure

Operation-NetGuard/
│
├── README.md
│
├── report/
│   └── Project_Report.pdf
│
└── packet-tracer/
    ├── README.md
    ├── Operation_NetGuard.pkt
    │
    └── screenshots/
        └── README.md

10. Project Outcome

Successfully designed and simulated a segmented enterprise network using VLANs, Router-on-a-Stick inter-VLAN routing and extended ACLs.

The implemented security policy restricted IT department access to the server network while maintaining HR connectivity. Connectivity tests and ACL match counters were used to verify the results.

11. Tools Used

- Cisco Packet Tracer
- Cisco IOS CLI
- IPv4 addressing
- VLANs and IEEE 802.1Q
- Extended Access Control Lists

12. Project Screenshots

"View All Project Screenshots" (packet-tracer/screenshots/)

13. Project Scope

This project is an educational network simulation designed to demonstrate enterprise network segmentation, inter-VLAN communication and access-control implementation. It is not a production deployment.

---

Project: Operation NetGuard
Category: Networking and Network Security
Platform: Cisco Packet Tracer
