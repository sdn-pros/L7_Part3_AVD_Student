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
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

## Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision | Serial Number |
| --- | ---- | ---- | ------------- | -------- | -------------------------- | ------------- |
| DC1 | l3leaf | BL1-DC1 | 192.168.0.91/24 | cEOS | Provisioned | - |
| DC2 | l3leaf | BL1-DC2 | 192.168.0.95/24 | cEOS | Provisioned | - |
| DC1 | l3leaf | leaf1-DC1 | 192.168.0.21/24 | cEOS | Provisioned | - |
| DC2 | l3leaf | leaf1-DC2 | 192.168.0.31/24 | cEOS | Provisioned | - |
| DC1 | l3leaf | leaf2-DC1 | 192.168.0.22/24 | cEOS | Provisioned | - |
| DC2 | l3leaf | leaf2-DC2 | 192.168.0.32/24 | cEOS | Provisioned | - |
| DC1 | l3leaf | leaf3-DC1 | 192.168.0.23/24 | cEOS | Provisioned | - |
| DC2 | l3leaf | leaf3-DC2 | 192.168.0.33/24 | cEOS | Provisioned | - |
| DC1 | l3leaf | leaf4-DC1 | 192.168.0.24/24 | cEOS | Provisioned | - |
| DC2 | l3leaf | leaf4-DC2 | 192.168.0.34/24 | cEOS | Provisioned | - |
| DC1 | spine | spine1-DC1 | 192.168.0.11/24 | cEOS | Provisioned | - |
| DC2 | spine | spine1-DC2 | 192.168.0.14/24 | cEOS | Provisioned | - |
| DC1 | spine | spine2-DC1 | 192.168.0.12/24 | cEOS | Provisioned | - |
| DC2 | spine | spine2-DC2 | 192.168.0.15/24 | cEOS | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l3leaf | BL1-DC1 | Ethernet6 | spine | spine1-DC1 | Ethernet6 |
| l3leaf | BL1-DC1 | Ethernet7 | spine | spine2-DC1 | Ethernet6 |
| l3leaf | BL1-DC2 | Ethernet6 | spine | spine1-DC2 | Ethernet6 |
| l3leaf | BL1-DC2 | Ethernet7 | spine | spine2-DC2 | Ethernet6 |
| l3leaf | leaf1-DC1 | Ethernet1 | mlag_peer | leaf2-DC1 | Ethernet1 |
| l3leaf | leaf1-DC1 | Ethernet2 | mlag_peer | leaf2-DC1 | Ethernet2 |
| l3leaf | leaf1-DC1 | Ethernet3 | spine | spine1-DC1 | Ethernet2 |
| l3leaf | leaf1-DC1 | Ethernet4 | spine | spine2-DC1 | Ethernet2 |
| l3leaf | leaf1-DC2 | Ethernet1 | mlag_peer | leaf2-DC2 | Ethernet1 |
| l3leaf | leaf1-DC2 | Ethernet2 | mlag_peer | leaf2-DC2 | Ethernet2 |
| l3leaf | leaf1-DC2 | Ethernet3 | spine | spine1-DC2 | Ethernet2 |
| l3leaf | leaf1-DC2 | Ethernet4 | spine | spine2-DC2 | Ethernet2 |
| l3leaf | leaf2-DC1 | Ethernet3 | spine | spine1-DC1 | Ethernet3 |
| l3leaf | leaf2-DC1 | Ethernet4 | spine | spine2-DC1 | Ethernet3 |
| l3leaf | leaf2-DC2 | Ethernet3 | spine | spine1-DC2 | Ethernet3 |
| l3leaf | leaf2-DC2 | Ethernet4 | spine | spine2-DC2 | Ethernet3 |
| l3leaf | leaf3-DC1 | Ethernet1 | mlag_peer | leaf4-DC1 | Ethernet1 |
| l3leaf | leaf3-DC1 | Ethernet2 | mlag_peer | leaf4-DC1 | Ethernet2 |
| l3leaf | leaf3-DC1 | Ethernet3 | spine | spine1-DC1 | Ethernet4 |
| l3leaf | leaf3-DC1 | Ethernet4 | spine | spine2-DC1 | Ethernet4 |
| l3leaf | leaf3-DC2 | Ethernet1 | mlag_peer | leaf4-DC2 | Ethernet1 |
| l3leaf | leaf3-DC2 | Ethernet2 | mlag_peer | leaf4-DC2 | Ethernet2 |
| l3leaf | leaf3-DC2 | Ethernet3 | spine | spine1-DC2 | Ethernet4 |
| l3leaf | leaf3-DC2 | Ethernet4 | spine | spine2-DC2 | Ethernet4 |
| l3leaf | leaf4-DC1 | Ethernet3 | spine | spine1-DC1 | Ethernet5 |
| l3leaf | leaf4-DC1 | Ethernet4 | spine | spine2-DC1 | Ethernet5 |
| l3leaf | leaf4-DC2 | Ethernet3 | spine | spine1-DC2 | Ethernet5 |
| l3leaf | leaf4-DC2 | Ethernet4 | spine | spine2-DC2 | Ethernet5 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 172.31.200.0/24 | 256 | 20 | 7.82 % |
| 192.168.103.0/24 | 256 | 20 | 7.82 % |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| BL1-DC1 | Ethernet6 | 192.168.103.17/31 | spine1-DC1 | Ethernet6 | 192.168.103.16/31 |
| BL1-DC1 | Ethernet7 | 192.168.103.19/31 | spine2-DC1 | Ethernet6 | 192.168.103.18/31 |
| BL1-DC2 | Ethernet6 | 172.31.200.17/31 | spine1-DC2 | Ethernet6 | 172.31.200.16/31 |
| BL1-DC2 | Ethernet7 | 172.31.200.19/31 | spine2-DC2 | Ethernet6 | 172.31.200.18/31 |
| leaf1-DC1 | Ethernet3 | 192.168.103.1/31 | spine1-DC1 | Ethernet2 | 192.168.103.0/31 |
| leaf1-DC1 | Ethernet4 | 192.168.103.3/31 | spine2-DC1 | Ethernet2 | 192.168.103.2/31 |
| leaf1-DC2 | Ethernet3 | 172.31.200.1/31 | spine1-DC2 | Ethernet2 | 172.31.200.0/31 |
| leaf1-DC2 | Ethernet4 | 172.31.200.3/31 | spine2-DC2 | Ethernet2 | 172.31.200.2/31 |
| leaf2-DC1 | Ethernet3 | 192.168.103.5/31 | spine1-DC1 | Ethernet3 | 192.168.103.4/31 |
| leaf2-DC1 | Ethernet4 | 192.168.103.7/31 | spine2-DC1 | Ethernet3 | 192.168.103.6/31 |
| leaf2-DC2 | Ethernet3 | 172.31.200.5/31 | spine1-DC2 | Ethernet3 | 172.31.200.4/31 |
| leaf2-DC2 | Ethernet4 | 172.31.200.7/31 | spine2-DC2 | Ethernet3 | 172.31.200.6/31 |
| leaf3-DC1 | Ethernet3 | 192.168.103.9/31 | spine1-DC1 | Ethernet4 | 192.168.103.8/31 |
| leaf3-DC1 | Ethernet4 | 192.168.103.11/31 | spine2-DC1 | Ethernet4 | 192.168.103.10/31 |
| leaf3-DC2 | Ethernet3 | 172.31.200.9/31 | spine1-DC2 | Ethernet4 | 172.31.200.8/31 |
| leaf3-DC2 | Ethernet4 | 172.31.200.11/31 | spine2-DC2 | Ethernet4 | 172.31.200.10/31 |
| leaf4-DC1 | Ethernet3 | 192.168.103.13/31 | spine1-DC1 | Ethernet5 | 192.168.103.12/31 |
| leaf4-DC1 | Ethernet4 | 192.168.103.15/31 | spine2-DC1 | Ethernet5 | 192.168.103.14/31 |
| leaf4-DC2 | Ethernet3 | 172.31.200.13/31 | spine1-DC2 | Ethernet5 | 172.31.200.12/31 |
| leaf4-DC2 | Ethernet4 | 172.31.200.15/31 | spine2-DC2 | Ethernet5 | 172.31.200.14/31 |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 192.168.100.0/24 | 256 | 7 | 2.74 % |
| 192.168.200.0/24 | 256 | 7 | 2.74 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| DC1 | BL1-DC1 | 192.168.100.5/32 |
| DC2 | BL1-DC2 | 192.168.200.7/32 |
| DC1 | leaf1-DC1 | 192.168.100.1/32 |
| DC2 | leaf1-DC2 | 192.168.200.3/32 |
| DC1 | leaf2-DC1 | 192.168.100.2/32 |
| DC2 | leaf2-DC2 | 192.168.200.4/32 |
| DC1 | leaf3-DC1 | 192.168.100.3/32 |
| DC2 | leaf3-DC2 | 192.168.200.5/32 |
| DC1 | leaf4-DC1 | 192.168.100.4/32 |
| DC2 | leaf4-DC2 | 192.168.200.6/32 |
| DC1 | spine1-DC1 | 192.168.100.1/32 |
| DC2 | spine1-DC2 | 192.168.200.1/32 |
| DC1 | spine2-DC1 | 192.168.100.2/32 |
| DC2 | spine2-DC2 | 192.168.200.2/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |
| 192.168.101.0/24 | 256 | 5 | 1.96 % |
| 192.168.202.0/24 | 256 | 5 | 1.96 % |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| DC1 | BL1-DC1 | 192.168.101.5/32 |
| DC2 | BL1-DC2 | 192.168.202.7/32 |
| DC1 | leaf1-DC1 | 192.168.101.1/32 |
| DC2 | leaf1-DC2 | 192.168.202.3/32 |
| DC1 | leaf2-DC1 | 192.168.101.1/32 |
| DC2 | leaf2-DC2 | 192.168.202.3/32 |
| DC1 | leaf3-DC1 | 192.168.101.3/32 |
| DC2 | leaf3-DC2 | 192.168.202.5/32 |
| DC1 | leaf4-DC1 | 192.168.101.3/32 |
| DC2 | leaf4-DC2 | 192.168.202.5/32 |
