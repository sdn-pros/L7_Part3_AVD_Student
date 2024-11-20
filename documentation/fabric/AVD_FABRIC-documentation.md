# AVD_FABRIC

## Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [ISIS CLNS interfaces](#isis-clns-interfaces)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

## Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision | Serial Number |
| --- | ---- | ---- | ------------- | -------- | -------------------------- | ------------- |
| AVD_FABRIC | pe | BL1-DC1 | 192.168.0.91/24 | vEOS-lab | Provisioned | - |
| AVD_FABRIC | pe | BL1-DC2 | 192.168.0.95/24 | vEOS-lab | Provisioned | - |
| DC1 | l3leaf | leaf1-DC1 | 192.168.0.21/24 | cEOS | Provisioned | - |
| DC2 | l3leaf | leaf1-DC2 | 192.168.0.31/24 | cEOS | Provisioned | - |
| DC1 | l3leaf | leaf2-DC1 | 192.168.0.22/24 | cEOS | Provisioned | - |
| DC2 | l3leaf | leaf2-DC2 | 192.168.0.32/24 | cEOS | Provisioned | - |
| DC1 | l3leaf | leaf3-DC1 | 192.168.0.23/24 | cEOS | Provisioned | - |
| DC2 | l3leaf | leaf3-DC2 | 192.168.0.33/24 | cEOS | Provisioned | - |
| DC1 | l3leaf | leaf4-DC1 | 192.168.0.24/24 | cEOS | Provisioned | - |
| DC2 | l3leaf | leaf4-DC2 | 192.168.0.34/24 | cEOS | Provisioned | - |
| AVD_FABRIC | p | P1 | 192.168.0.93/24 | cEOS | Provisioned | - |
| AVD_FABRIC | p | P2 | 192.168.0.94/24 | cEOS | Provisioned | - |
| AVD_FABRIC | p | P3 | 192.168.0.97/24 | cEOS | Provisioned | - |
| AVD_FABRIC | p | P4 | 192.168.0.98/24 | cEOS | Provisioned | - |
| AVD_FABRIC | rr | RR | 192.168.0.90/24 | vEOS-lab | Provisioned | - |
| DC1 | spine | spine1-DC1 | 192.168.0.11/24 | cEOS | Provisioned | - |
| DC2 | spine | spine1-DC2 | 192.168.0.14/24 | cEOS | Provisioned | - |
| DC1 | spine | spine2-DC1 | 192.168.0.12/24 | cEOS | Provisioned | - |
| DC2 | spine | spine2-DC2 | 192.168.0.15/24 | cEOS | Provisioned | - |
| DC1 | spine | spine3-DC1 | 192.168.0.13/24 | cEOS | Provisioned | - |
| DC2 | spine | spine3-DC2 | 192.168.0.16/24 | cEOS | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| pe | BL1-DC1 | Ethernet1 | p | P1 | Ethernet1 |
| pe | BL1-DC1 | Ethernet4 | p | P2 | Ethernet3 |
| pe | BL1-DC1 | Ethernet5 | rr | RR | Ethernet1 |
| pe | BL1-DC2 | Ethernet1 | p | P3 | Ethernet1 |
| pe | BL1-DC2 | Ethernet4 | p | P4 | Ethernet3 |
| pe | BL1-DC2 | Ethernet5 | rr | RR | Ethernet5 |
| l3leaf | leaf1-DC1 | Ethernet1 | mlag_peer | leaf2-DC1 | Ethernet1 |
| l3leaf | leaf1-DC1 | Ethernet2 | mlag_peer | leaf2-DC1 | Ethernet2 |
| l3leaf | leaf1-DC1 | Ethernet3 | spine | spine1-DC1 | Ethernet2 |
| l3leaf | leaf1-DC1 | Ethernet4 | spine | spine2-DC1 | Ethernet2 |
| l3leaf | leaf1-DC1 | Ethernet5 | spine | spine3-DC1 | Ethernet2 |
| l3leaf | leaf1-DC2 | Ethernet1 | mlag_peer | leaf2-DC2 | Ethernet1 |
| l3leaf | leaf1-DC2 | Ethernet2 | mlag_peer | leaf2-DC2 | Ethernet2 |
| l3leaf | leaf1-DC2 | Ethernet3 | spine | spine1-DC2 | Ethernet2 |
| l3leaf | leaf1-DC2 | Ethernet4 | spine | spine2-DC2 | Ethernet2 |
| l3leaf | leaf1-DC2 | Ethernet5 | spine | spine3-DC2 | Ethernet2 |
| l3leaf | leaf2-DC1 | Ethernet3 | spine | spine1-DC1 | Ethernet3 |
| l3leaf | leaf2-DC1 | Ethernet4 | spine | spine2-DC1 | Ethernet3 |
| l3leaf | leaf2-DC1 | Ethernet5 | spine | spine3-DC1 | Ethernet3 |
| l3leaf | leaf2-DC2 | Ethernet3 | spine | spine1-DC2 | Ethernet3 |
| l3leaf | leaf2-DC2 | Ethernet4 | spine | spine2-DC2 | Ethernet3 |
| l3leaf | leaf2-DC2 | Ethernet5 | spine | spine3-DC2 | Ethernet3 |
| l3leaf | leaf3-DC1 | Ethernet1 | mlag_peer | leaf4-DC1 | Ethernet1 |
| l3leaf | leaf3-DC1 | Ethernet2 | mlag_peer | leaf4-DC1 | Ethernet2 |
| l3leaf | leaf3-DC1 | Ethernet3 | spine | spine1-DC1 | Ethernet4 |
| l3leaf | leaf3-DC1 | Ethernet4 | spine | spine2-DC1 | Ethernet4 |
| l3leaf | leaf3-DC1 | Ethernet5 | spine | spine3-DC1 | Ethernet4 |
| l3leaf | leaf3-DC2 | Ethernet1 | mlag_peer | leaf4-DC2 | Ethernet1 |
| l3leaf | leaf3-DC2 | Ethernet2 | mlag_peer | leaf4-DC2 | Ethernet2 |
| l3leaf | leaf3-DC2 | Ethernet3 | spine | spine1-DC2 | Ethernet4 |
| l3leaf | leaf3-DC2 | Ethernet4 | spine | spine2-DC2 | Ethernet4 |
| l3leaf | leaf3-DC2 | Ethernet5 | spine | spine3-DC2 | Ethernet4 |
| l3leaf | leaf4-DC1 | Ethernet3 | spine | spine1-DC1 | Ethernet5 |
| l3leaf | leaf4-DC1 | Ethernet4 | spine | spine2-DC1 | Ethernet5 |
| l3leaf | leaf4-DC1 | Ethernet5 | spine | spine3-DC1 | Ethernet5 |
| l3leaf | leaf4-DC2 | Ethernet3 | spine | spine1-DC2 | Ethernet5 |
| l3leaf | leaf4-DC2 | Ethernet4 | spine | spine2-DC2 | Ethernet5 |
| l3leaf | leaf4-DC2 | Ethernet5 | spine | spine3-DC2 | Ethernet5 |
| p | P1 | Ethernet2 | p | P3 | Ethernet2 |
| p | P1 | Ethernet4 | p | P2 | Ethernet4 |
| p | P2 | Ethernet2 | p | P4 | Ethernet2 |
| p | P3 | Ethernet4 | p | P4 | Ethernet4 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| BL1-DC1 | Ethernet1 | 10.1.11.2/30 | P1 | Ethernet1 | 10.1.11.1/30 |
| BL1-DC1 | Ethernet4 | 10.2.11.2/30 | P2 | Ethernet3 | 10.2.11.1/30 |
| BL1-DC1 | Ethernet5 | 10.11.90.1/30 | RR | Ethernet1 | 10.11.90.2/30 |
| BL1-DC2 | Ethernet1 | 10.3.21.2/30 | P3 | Ethernet1 | 10.3.21.1/30 |
| BL1-DC2 | Ethernet4 | 10.4.21.2/30 | P4 | Ethernet3 | 10.4.21.1/30 |
| BL1-DC2 | Ethernet5 | 10.21.90.1/30 | RR | Ethernet5 | 10.21.90.2/30 |
| leaf1-DC1 | Ethernet3 | 10.10.0.1/31 | spine1-DC1 | Ethernet2 | 10.10.0.0/31 |
| leaf1-DC1 | Ethernet4 | 10.10.0.33/31 | spine2-DC1 | Ethernet2 | 10.10.0.32/31 |
| leaf1-DC1 | Ethernet5 | 10.10.0.65/31 | spine3-DC1 | Ethernet2 | 10.10.0.64/31 |
| leaf1-DC2 | Ethernet3 | 10.20.0.1/31 | spine1-DC2 | Ethernet2 | 10.20.0.0/31 |
| leaf1-DC2 | Ethernet4 | 10.20.0.33/31 | spine2-DC2 | Ethernet2 | 10.20.0.32/31 |
| leaf1-DC2 | Ethernet5 | 10.20.0.65/31 | spine3-DC2 | Ethernet2 | 10.20.0.64/31 |
| leaf2-DC1 | Ethernet3 | 10.10.0.3/31 | spine1-DC1 | Ethernet3 | 10.10.0.2/31 |
| leaf2-DC1 | Ethernet4 | 10.10.0.35/31 | spine2-DC1 | Ethernet3 | 10.10.0.34/31 |
| leaf2-DC1 | Ethernet5 | 10.10.0.67/31 | spine3-DC1 | Ethernet3 | 10.10.0.66/31 |
| leaf2-DC2 | Ethernet3 | 10.20.0.3/31 | spine1-DC2 | Ethernet3 | 10.20.0.2/31 |
| leaf2-DC2 | Ethernet4 | 10.20.0.35/31 | spine2-DC2 | Ethernet3 | 10.20.0.34/31 |
| leaf2-DC2 | Ethernet5 | 10.20.0.67/31 | spine3-DC2 | Ethernet3 | 10.20.0.66/31 |
| leaf3-DC1 | Ethernet3 | 10.10.0.5/31 | spine1-DC1 | Ethernet4 | 10.10.0.4/31 |
| leaf3-DC1 | Ethernet4 | 10.10.0.37/31 | spine2-DC1 | Ethernet4 | 10.10.0.36/31 |
| leaf3-DC1 | Ethernet5 | 10.10.0.69/31 | spine3-DC1 | Ethernet4 | 10.10.0.68/31 |
| leaf3-DC2 | Ethernet3 | 10.20.0.5/31 | spine1-DC2 | Ethernet4 | 10.20.0.4/31 |
| leaf3-DC2 | Ethernet4 | 10.20.0.37/31 | spine2-DC2 | Ethernet4 | 10.20.0.36/31 |
| leaf3-DC2 | Ethernet5 | 10.20.0.69/31 | spine3-DC2 | Ethernet4 | 10.20.0.68/31 |
| leaf4-DC1 | Ethernet3 | 10.10.0.7/31 | spine1-DC1 | Ethernet5 | 10.10.0.6/31 |
| leaf4-DC1 | Ethernet4 | 10.10.0.39/31 | spine2-DC1 | Ethernet5 | 10.10.0.38/31 |
| leaf4-DC1 | Ethernet5 | 10.10.0.71/31 | spine3-DC1 | Ethernet5 | 10.10.0.70/31 |
| leaf4-DC2 | Ethernet3 | 10.20.0.7/31 | spine1-DC2 | Ethernet5 | 10.20.0.6/31 |
| leaf4-DC2 | Ethernet4 | 10.20.0.39/31 | spine2-DC2 | Ethernet5 | 10.20.0.38/31 |
| leaf4-DC2 | Ethernet5 | 10.20.0.71/31 | spine3-DC2 | Ethernet5 | 10.20.0.70/31 |
| P1 | Ethernet2 | 10.1.3.1/30 | P3 | Ethernet2 | 10.1.3.2/30 |
| P1 | Ethernet4 | 10.1.2.1/30 | P2 | Ethernet4 | 10.1.2.2/30 |
| P2 | Ethernet2 | 10.2.4.1/30 | P4 | Ethernet2 | 10.2.4.2/30 |
| P3 | Ethernet4 | 10.3.4.1/30 | P4 | Ethernet4 | 10.3.4.2/30 |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 192.168.255.0/24 | 256 | 21 | 8.21 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| AVD_FABRIC | BL1-DC1 | 192.168.255.91/32 |
| AVD_FABRIC | BL1-DC2 | 192.168.255.95/32 |
| DC1 | leaf1-DC1 | 192.168.255.21/32 |
| DC2 | leaf1-DC2 | 192.168.255.31/32 |
| DC1 | leaf2-DC1 | 192.168.255.22/32 |
| DC2 | leaf2-DC2 | 192.168.255.32/32 |
| DC1 | leaf3-DC1 | 192.168.255.23/32 |
| DC2 | leaf3-DC2 | 192.168.255.33/32 |
| DC1 | leaf4-DC1 | 192.168.255.24/32 |
| DC2 | leaf4-DC2 | 192.168.255.34/32 |
| AVD_FABRIC | P1 | 192.168.255.93/32 |
| AVD_FABRIC | P2 | 192.168.255.94/32 |
| AVD_FABRIC | P3 | 192.168.255.97/32 |
| AVD_FABRIC | P4 | 192.168.255.98/32 |
| AVD_FABRIC | RR | 192.168.255.90/32 |
| DC1 | spine1-DC1 | 192.168.255.11/32 |
| DC2 | spine1-DC2 | 192.168.255.14/32 |
| DC1 | spine2-DC1 | 192.168.255.12/32 |
| DC2 | spine2-DC2 | 192.168.255.15/32 |
| DC1 | spine3-DC1 | 192.168.255.13/32 |
| DC2 | spine3-DC2 | 192.168.255.16/32 |

### ISIS CLNS interfaces

| POD | Node | CLNS Address |
| --- | ---- | ------------ |
| AVD_FABRIC | BL1-DC1 | 49.0001.0000.0001.0091.00 |
| AVD_FABRIC | BL1-DC2 | 49.0001.0000.0001.0095.00 |
| AVD_FABRIC | P1 | 49.0001.0000.0000.0093.00 |
| AVD_FABRIC | P2 | 49.0001.0000.0000.0094.00 |
| AVD_FABRIC | P3 | 49.0001.0000.0000.0097.00 |
| AVD_FABRIC | P4 | 49.0001.0000.0000.0098.00 |
| AVD_FABRIC | RR | 49.0001.0000.0002.0090.00 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |
| 10.255.1.0/24 | 256 | 10 | 3.91 % |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| AVD_FABRIC | BL1-DC1 | 10.255.1.91/32 |
| AVD_FABRIC | BL1-DC2 | 10.255.1.95/32 |
| DC1 | leaf1-DC1 | 10.255.1.21/32 |
| DC2 | leaf1-DC2 | 10.255.1.31/32 |
| DC1 | leaf2-DC1 | 10.255.1.21/32 |
| DC2 | leaf2-DC2 | 10.255.1.31/32 |
| DC1 | leaf3-DC1 | 10.255.1.23/32 |
| DC2 | leaf3-DC2 | 10.255.1.33/32 |
| DC1 | leaf4-DC1 | 10.255.1.23/32 |
| DC2 | leaf4-DC2 | 10.255.1.33/32 |
