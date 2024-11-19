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
| DC1 | gwleaf | BL1-DC1 | 192.168.0.91/24 | cEOS | Provisioned | - |
| DC1 | l3leaf | leaf1-DC1 | 192.168.0.21/24 | cEOS | Provisioned | - |
| DC1 | l3leaf | leaf2-DC1 | 192.168.0.22/24 | cEOS | Provisioned | - |
| DC1 | l3leaf | leaf3-DC1 | 192.168.0.23/24 | cEOS | Provisioned | - |
| DC1 | l3leaf | leaf4-DC1 | 192.168.0.24/24 | cEOS | Provisioned | - |
| DC1 | spine | spine1-DC1 | 192.168.0.11/24 | cEOS | Provisioned | - |
| DC1 | spine | spine2-DC1 | 192.168.0.12/24 | cEOS | Provisioned | - |
| DC1 | spine | spine3-DC1 | 192.168.0.13/24 | cEOS | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| gwleaf | BL1-DC1 | Ethernet6 | spine | spine1-DC1 | Ethernet6 |
| gwleaf | BL1-DC1 | Ethernet7 | spine | spine2-DC1 | Ethernet6 |
| gwleaf | BL1-DC1 | Ethernet8 | spine | spine3-DC1 | Ethernet6 |
| l3leaf | leaf1-DC1 | Ethernet1 | mlag_peer | leaf2-DC1 | Ethernet1 |
| l3leaf | leaf1-DC1 | Ethernet2 | mlag_peer | leaf2-DC1 | Ethernet2 |
| l3leaf | leaf1-DC1 | Ethernet3 | spine | spine1-DC1 | Ethernet2 |
| l3leaf | leaf1-DC1 | Ethernet4 | spine | spine2-DC1 | Ethernet2 |
| l3leaf | leaf1-DC1 | Ethernet5 | spine | spine3-DC1 | Ethernet2 |
| l3leaf | leaf2-DC1 | Ethernet3 | spine | spine1-DC1 | Ethernet3 |
| l3leaf | leaf2-DC1 | Ethernet4 | spine | spine2-DC1 | Ethernet3 |
| l3leaf | leaf2-DC1 | Ethernet5 | spine | spine3-DC1 | Ethernet3 |
| l3leaf | leaf3-DC1 | Ethernet1 | mlag_peer | leaf4-DC1 | Ethernet1 |
| l3leaf | leaf3-DC1 | Ethernet2 | mlag_peer | leaf4-DC1 | Ethernet2 |
| l3leaf | leaf3-DC1 | Ethernet3 | spine | spine1-DC1 | Ethernet4 |
| l3leaf | leaf3-DC1 | Ethernet4 | spine | spine2-DC1 | Ethernet4 |
| l3leaf | leaf3-DC1 | Ethernet5 | spine | spine3-DC1 | Ethernet4 |
| l3leaf | leaf4-DC1 | Ethernet3 | spine | spine1-DC1 | Ethernet5 |
| l3leaf | leaf4-DC1 | Ethernet4 | spine | spine2-DC1 | Ethernet5 |
| l3leaf | leaf4-DC1 | Ethernet5 | spine | spine3-DC1 | Ethernet5 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| BL1-DC1 | Ethernet6 | 10.111.11.1/31 | spine1-DC1 | Ethernet6 | 10.111.11.0/31 |
| BL1-DC1 | Ethernet7 | 10.112.11.1/31 | spine2-DC1 | Ethernet6 | 10.112.11.0/31 |
| BL1-DC1 | Ethernet8 | 10.113.11.1/31 | spine3-DC1 | Ethernet6 | 10.113.11.0/31 |
| leaf1-DC1 | Ethernet3 | 10.10.0.1/31 | spine1-DC1 | Ethernet2 | 10.10.0.0/31 |
| leaf1-DC1 | Ethernet4 | 10.10.0.33/31 | spine2-DC1 | Ethernet2 | 10.10.0.32/31 |
| leaf1-DC1 | Ethernet5 | 10.10.0.65/31 | spine3-DC1 | Ethernet2 | 10.10.0.64/31 |
| leaf2-DC1 | Ethernet3 | 10.10.0.3/31 | spine1-DC1 | Ethernet3 | 10.10.0.2/31 |
| leaf2-DC1 | Ethernet4 | 10.10.0.35/31 | spine2-DC1 | Ethernet3 | 10.10.0.34/31 |
| leaf2-DC1 | Ethernet5 | 10.10.0.67/31 | spine3-DC1 | Ethernet3 | 10.10.0.66/31 |
| leaf3-DC1 | Ethernet3 | 10.10.0.5/31 | spine1-DC1 | Ethernet4 | 10.10.0.4/31 |
| leaf3-DC1 | Ethernet4 | 10.10.0.37/31 | spine2-DC1 | Ethernet4 | 10.10.0.36/31 |
| leaf3-DC1 | Ethernet5 | 10.10.0.69/31 | spine3-DC1 | Ethernet4 | 10.10.0.68/31 |
| leaf4-DC1 | Ethernet3 | 10.10.0.7/31 | spine1-DC1 | Ethernet5 | 10.10.0.6/31 |
| leaf4-DC1 | Ethernet4 | 10.10.0.39/31 | spine2-DC1 | Ethernet5 | 10.10.0.38/31 |
| leaf4-DC1 | Ethernet5 | 10.10.0.71/31 | spine3-DC1 | Ethernet5 | 10.10.0.70/31 |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 192.168.255.0/24 | 256 | 8 | 3.13 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| DC1 | BL1-DC1 | 192.168.255.91/32 |
| DC1 | leaf1-DC1 | 192.168.255.21/32 |
| DC1 | leaf2-DC1 | 192.168.255.22/32 |
| DC1 | leaf3-DC1 | 192.168.255.23/32 |
| DC1 | leaf4-DC1 | 192.168.255.24/32 |
| DC1 | spine1-DC1 | 192.168.255.11/32 |
| DC1 | spine2-DC1 | 192.168.255.12/32 |
| DC1 | spine3-DC1 | 192.168.255.13/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |
| 10.255.1.0/24 | 256 | 5 | 1.96 % |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| DC1 | BL1-DC1 | 10.255.1.91/32 |
| DC1 | leaf1-DC1 | 10.255.1.21/32 |
| DC1 | leaf2-DC1 | 10.255.1.21/32 |
| DC1 | leaf3-DC1 | 10.255.1.23/32 |
| DC1 | leaf4-DC1 | 10.255.1.23/32 |
