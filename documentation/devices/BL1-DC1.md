# BL1-DC1

## Table of Contents

- [Management](#management)
  - [Management Interfaces](#management-interfaces)
  - [DNS Domain](#dns-domain)
  - [Management API HTTP](#management-api-http)
- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [Internal VLAN Allocation Policy](#internal-vlan-allocation-policy)
  - [Internal VLAN Allocation Policy Summary](#internal-vlan-allocation-policy-summary)
  - [Internal VLAN Allocation Policy Device Configuration](#internal-vlan-allocation-policy-device-configuration)
- [VLANs](#vlans)
  - [VLANs Summary](#vlans-summary)
  - [VLANs Device Configuration](#vlans-device-configuration)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
  - [VLAN Interfaces](#vlan-interfaces)
  - [VXLAN Interface](#vxlan-interface)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [Virtual Router MAC Address](#virtual-router-mac-address)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Static Routes](#static-routes)
  - [Router ISIS](#router-isis)
  - [Router BGP](#router-bgp)
- [BFD](#bfd)
  - [Router BFD](#router-bfd)
- [MPLS](#mpls)
  - [MPLS and LDP](#mpls-and-ldp)
  - [MPLS Interfaces](#mpls-interfaces)
- [Multicast](#multicast)
  - [IP IGMP Snooping](#ip-igmp-snooping)
- [Filters](#filters)
  - [Route-maps](#route-maps)
  - [IP Extended Community Lists](#ip-extended-community-lists)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)

## Management

### Management Interfaces

#### Management Interfaces Summary

##### IPv4

| Management Interface | Description | Type | VRF | IP Address | Gateway |
| -------------------- | ----------- | ---- | --- | ---------- | ------- |
| Management0 | oob_management | oob | MGMT | 192.168.0.91/24 | 192.168.0.1 |

##### IPv6

| Management Interface | Description | Type | VRF | IPv6 Address | IPv6 Gateway |
| -------------------- | ----------- | ---- | --- | ------------ | ------------ |
| Management0 | oob_management | oob | MGMT | - | - |

#### Management Interfaces Device Configuration

```eos
!
interface Management0
   description oob_management
   no shutdown
   vrf MGMT
   ip address 192.168.0.91/24
```

### DNS Domain

DNS domain: atd.lab

#### DNS Domain Device Configuration

```eos
dns domain atd.lab
!
```

### Management API HTTP

#### Management API HTTP Summary

| HTTP | HTTPS | Default Services |
| ---- | ----- | ---------------- |
| False | True | - |

#### Management API VRF Access

| VRF Name | IPv4 ACL | IPv6 ACL |
| -------- | -------- | -------- |
| MGMT | - | - |

#### Management API HTTP Device Configuration

```eos
!
management api http-commands
   protocol https
   no shutdown
   !
   vrf MGMT
      no shutdown
```

## Spanning Tree

### Spanning Tree Summary

STP mode: **mstp**

### Spanning Tree Device Configuration

```eos
!
spanning-tree mode mstp
```

## Internal VLAN Allocation Policy

### Internal VLAN Allocation Policy Summary

| Policy Allocation | Range Beginning | Range Ending |
| ------------------| --------------- | ------------ |
| ascending | 1006 | 1199 |

### Internal VLAN Allocation Policy Device Configuration

```eos
!
vlan internal order ascending range 1006 1199
```

## VLANs

### VLANs Summary

| VLAN ID | Name | Trunk Groups |
| ------- | ---- | ------------ |
| 16 | VLAN16 | - |
| 17 | VLAN17 | - |

### VLANs Device Configuration

```eos
!
vlan 16
   name VLAN16
!
vlan 17
   name VLAN17
```

## Interfaces

### Ethernet Interfaces

#### Ethernet Interfaces Summary

##### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |

*Inherited from Port-Channel Interface

##### IPv4

| Interface | Description | Type | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | -----| ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet1 | P2P_LINK_TO_P1_Ethernet1 | routed | - | 10.1.11.2/30 | default | 9214 | False | - | - |
| Ethernet4 | P2P_LINK_TO_P2_Ethernet3 | routed | - | 10.2.11.2/30 | default | 9214 | False | - | - |
| Ethernet5 | P2P_LINK_TO_RR_Ethernet1 | routed | - | 10.11.90.1/30 | default | 9214 | False | - | - |
| Ethernet6 | - | routed | - | 10.111.11.1/31 | default | - | False | - | - |
| Ethernet7 | - | routed | - | 10.112.11.1/31 | default | - | False | - | - |
| Ethernet8 | - | routed | - | 10.113.11.1/31 | default | - | False | - | - |

##### ISIS

| Interface | Channel Group | ISIS Instance | ISIS BFD | ISIS Metric | Mode | ISIS Circuit Type | Hello Padding | Authentication Mode |
| --------- | ------------- | ------------- | -------- | ----------- | ---- | ----------------- | ------------- | ------------------- |
| Ethernet1 | - | bb | - | 100 | point-to-point | level-2 | True | - |
| Ethernet4 | - | bb | - | 100 | point-to-point | level-2 | True | - |
| Ethernet5 | - | bb | - | 100 | point-to-point | level-2 | True | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description P2P_LINK_TO_P1_Ethernet1
   no shutdown
   mtu 9214
   no switchport
   ip address 10.1.11.2/30
   mpls ip
   isis enable bb
   isis circuit-type level-2
   isis metric 100
   isis hello padding
   isis network point-to-point
!
interface Ethernet4
   description P2P_LINK_TO_P2_Ethernet3
   no shutdown
   mtu 9214
   no switchport
   ip address 10.2.11.2/30
   mpls ip
   isis enable bb
   isis circuit-type level-2
   isis metric 100
   isis hello padding
   isis network point-to-point
!
interface Ethernet5
   description P2P_LINK_TO_RR_Ethernet1
   no shutdown
   mtu 9214
   no switchport
   ip address 10.11.90.1/30
   mpls ip
   isis enable bb
   isis circuit-type level-2
   isis metric 100
   isis hello padding
   isis network point-to-point
!
interface Ethernet6
   no shutdown
   no switchport
   ip address 10.111.11.1/31
!
interface Ethernet7
   no shutdown
   no switchport
   ip address 10.112.11.1/31
!
interface Ethernet8
   no shutdown
   no switchport
   ip address 10.113.11.1/31
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | MPLS_Overlay_peering | default | 192.168.255.91/32 |
| Loopback1 | VTEP_VXLAN_Tunnel_Source | default | 10.255.1.91/32 |

##### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | MPLS_Overlay_peering | default | - |
| Loopback1 | VTEP_VXLAN_Tunnel_Source | default | - |

##### ISIS

| Interface | ISIS instance | ISIS metric | Interface mode |
| --------- | ------------- | ----------- | -------------- |
| Loopback0 | bb | - | passive |
| Loopback1 | bb | - | passive |

#### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description MPLS_Overlay_peering
   no shutdown
   ip address 192.168.255.91/32
   isis enable bb
   isis passive
   node-segment ipv4 index 91
!
interface Loopback1
   description VTEP_VXLAN_Tunnel_Source
   no shutdown
   ip address 10.255.1.91/32
   isis enable bb
   isis passive
```

### VLAN Interfaces

#### VLAN Interfaces Summary

| Interface | Description | VRF |  MTU | Shutdown |
| --------- | ----------- | --- | ---- | -------- |
| Vlan16 | VLAN16 | tenant-a | - | False |
| Vlan17 | VLAN17 | tenant-a | - | False |

##### IPv4

| Interface | VRF | IP Address | IP Address Virtual | IP Router Virtual Address | VRRP | ACL In | ACL Out |
| --------- | --- | ---------- | ------------------ | ------------------------- | ---- | ------ | ------- |
| Vlan16 |  tenant-a  |  -  |  172.16.16.254/24  |  -  |  -  |  -  |  -  |
| Vlan17 |  tenant-a  |  -  |  172.16.17.254/24  |  -  |  -  |  -  |  -  |

#### VLAN Interfaces Device Configuration

```eos
!
interface Vlan16
   description VLAN16
   no shutdown
   vrf tenant-a
   ip address virtual 172.16.16.254/24
!
interface Vlan17
   description VLAN17
   no shutdown
   vrf tenant-a
   ip address virtual 172.16.17.254/24
```

### VXLAN Interface

#### VXLAN Interface Summary

| Setting | Value |
| ------- | ----- |
| Source Interface | loopback0 |
| UDP port | 4789 |

##### VLAN to VNI, Flood List and Multicast Group Mappings

| VLAN | VNI | Flood List | Multicast Group |
| ---- | --- | ---------- | --------------- |
| 16 | 10016 | - | - |
| 17 | 10017 | - | - |

##### VRF to VNI and Multicast Group Mappings

| VRF | VNI | Multicast Group |
| ---- | --- | --------------- |
| tenant-a | 1000 | - |

#### VXLAN Interface Device Configuration

```eos
!
interface Vxlan1
   description BL1-DC1_VTEP
   vxlan source-interface loopback0
   vxlan udp-port 4789
   vxlan vlan 16 vni 10016
   vxlan vlan 17 vni 10017
   vxlan vrf tenant-a vni 1000
```

## Routing

### Service Routing Protocols Model

Multi agent routing protocol model enabled

```eos
!
service routing protocols model multi-agent
```

### Virtual Router MAC Address

#### Virtual Router MAC Address Summary

Virtual Router MAC Address: 00:1c:73:00:00:99

#### Virtual Router MAC Address Device Configuration

```eos
!
ip virtual-router mac-address 00:1c:73:00:00:99
```

### IP Routing

#### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | True |
| MGMT | True |
| tenant-a | True |

#### IP Routing Device Configuration

```eos
!
ip routing
ip routing vrf MGMT
ip routing vrf tenant-a
```

### IPv6 Routing

#### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | False |
| MGMT | false |
| tenant-a | false |

### Static Routes

#### Static Routes Summary

| VRF | Destination Prefix | Next Hop IP | Exit interface | Administrative Distance | Tag | Route Name | Metric |
| --- | ------------------ | ----------- | -------------- | ----------------------- | --- | ---------- | ------ |
| MGMT | 0.0.0.0/0 | 192.168.0.1 | - | 1 | - | - | - |

#### Static Routes Device Configuration

```eos
!
ip route vrf MGMT 0.0.0.0/0 192.168.0.1
```

### Router ISIS

#### Router ISIS Summary

| Settings | Value |
| -------- | ----- |
| Instance | bb |
| Net-ID | 49.0001.0000.0001.0091.00 |
| Type | level-2 |
| Router-ID | 192.168.255.91 |
| Log Adjacency Changes | True |
| SR MPLS Enabled | True |

#### ISIS Interfaces Summary

| Interface | ISIS Instance | ISIS Metric | Interface Mode |
| --------- | ------------- | ----------- | -------------- |
| Ethernet1 | bb | 100 | point-to-point |
| Ethernet4 | bb | 100 | point-to-point |
| Ethernet5 | bb | 100 | point-to-point |
| Loopback0 | bb | - | passive |
| Loopback1 | bb | - | passive |

#### ISIS Segment-routing Node-SID

| Loopback | IPv4 Index | IPv6 Index |
| -------- | ---------- | ---------- |
| Loopback0 | 91 | - |

#### ISIS IPv4 Address Family Summary

| Settings | Value |
| -------- | ----- |
| IPv4 Address-family Enabled | True |
| Maximum-paths | 4 |

#### Router ISIS Device Configuration

```eos
!
router isis bb
   net 49.0001.0000.0001.0091.00
   is-type level-2
   router-id ipv4 192.168.255.91
   log-adjacency-changes
   !
   address-family ipv4 unicast
      maximum-paths 4
   !
   segment-routing mpls
      no shutdown
```

### Router BGP

ASN Notation: asplain

#### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 1 | 192.168.255.91 |

| BGP Tuning |
| ---------- |
| no bgp default ipv4-unicast |
| distance bgp 20 200 200 |
| maximum-paths 4 ecmp 4 |

#### Router BGP Peer Groups

##### MPLS-OVERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | mpls |
| Remote AS | 1 |
| Source | Loopback0 |
| BFD | True |
| Send community | all |
| Maximum routes | 0 (no limit) |

##### VXLAN-OVERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Remote AS | 65110 |
| Source | Loopback0 |
| Ebgp multihop | 15 |
| Send community | all |

#### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD | RIB Pre-Policy Retain | Route-Reflector Client | Passive | TTL Max Hops |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- | --------------------- | ---------------------- | ------- | ------------ |
| 10.111.11.0 | 65110 | default | - | - | - | - | - | - | - | - | - |
| 10.112.11.0 | 65110 | default | - | - | - | - | - | - | - | - | - |
| 10.113.11.0 | 65110 | default | - | - | - | - | - | - | - | - | - |
| 192.168.255.11 | Inherited from peer group VXLAN-OVERLAY-PEERS | default | - | Inherited from peer group VXLAN-OVERLAY-PEERS | - | - | - | - | - | - | - |
| 192.168.255.12 | Inherited from peer group VXLAN-OVERLAY-PEERS | default | - | Inherited from peer group VXLAN-OVERLAY-PEERS | - | - | - | - | - | - | - |
| 192.168.255.13 | Inherited from peer group VXLAN-OVERLAY-PEERS | default | - | Inherited from peer group VXLAN-OVERLAY-PEERS | - | - | - | - | - | - | - |
| 192.168.255.95 | Inherited from peer group MPLS-OVERLAY-PEERS | default | - | Inherited from peer group MPLS-OVERLAY-PEERS | Inherited from peer group MPLS-OVERLAY-PEERS | - | Inherited from peer group MPLS-OVERLAY-PEERS | - | - | - | - |

#### Router BGP EVPN Address Family

##### EVPN Peer Groups

| Peer Group | Activate | Encapsulation |
| ---------- | -------- | ------------- |
| MPLS-OVERLAY-PEERS | True | default |
| VXLAN-OVERLAY-PEERS | True | vxlan |

##### EVPN Neighbor Default Encapsulation

| Neighbor Default Encapsulation | Next-hop-self Source Interface |
| ------------------------------ | ------------------------------ |
| mpls | Loopback0 |

#### Router BGP VLANs

| VLAN | Route-Distinguisher | Both Route-Target | Import Route Target | Export Route-Target | Redistribute |
| ---- | ------------------- | ----------------- | ------------------- | ------------------- | ------------ |
| 16 | 192.168.255.91:10016 | 10016:10016 | - | - | learned |
| 17 | 192.168.255.91:10017 | 10017:10017 | - | - | learned |

#### Router BGP VRFs

| VRF | Route-Distinguisher | Redistribute |
| --- | ------------------- | ------------ |
| tenant-a | 192.168.255.91:1000 | connected |

#### Router BGP Device Configuration

```eos
!
router bgp 1
   router-id 192.168.255.91
   distance bgp 20 200 200
   maximum-paths 4 ecmp 4
   no bgp default ipv4-unicast
   neighbor MPLS-OVERLAY-PEERS peer group
   neighbor MPLS-OVERLAY-PEERS remote-as 1
   neighbor MPLS-OVERLAY-PEERS update-source Loopback0
   neighbor MPLS-OVERLAY-PEERS bfd
   neighbor MPLS-OVERLAY-PEERS send-community
   neighbor MPLS-OVERLAY-PEERS maximum-routes 0
   neighbor VXLAN-OVERLAY-PEERS peer group
   neighbor VXLAN-OVERLAY-PEERS remote-as 65110
   neighbor VXLAN-OVERLAY-PEERS update-source Loopback0
   neighbor VXLAN-OVERLAY-PEERS ebgp-multihop 15
   neighbor VXLAN-OVERLAY-PEERS send-community
   neighbor 10.111.11.0 remote-as 65110
   neighbor 10.112.11.0 remote-as 65110
   neighbor 10.113.11.0 remote-as 65110
   neighbor 192.168.255.11 peer group VXLAN-OVERLAY-PEERS
   neighbor 192.168.255.12 peer group VXLAN-OVERLAY-PEERS
   neighbor 192.168.255.13 peer group VXLAN-OVERLAY-PEERS
   neighbor 192.168.255.95 peer group MPLS-OVERLAY-PEERS
   neighbor 192.168.255.95 description BL1-DC2
   !
   vlan 16
      rd 192.168.255.91:10016
      route-target both 10016:10016
      redistribute learned
   !
   vlan 17
      rd 192.168.255.91:10017
      route-target both 10017:10017
      redistribute learned
   !
   address-family evpn
      neighbor default encapsulation mpls next-hop-self source-interface Loopback0
      neighbor MPLS-OVERLAY-PEERS route-map RM-EVPN-SOO-IN in
      neighbor MPLS-OVERLAY-PEERS route-map RM-EVPN-SOO-OUT out
      neighbor MPLS-OVERLAY-PEERS activate
      neighbor VXLAN-OVERLAY-PEERS activate
      neighbor VXLAN-OVERLAY-PEERS encapsulation vxlan
   !
   address-family ipv4
      no neighbor MPLS-OVERLAY-PEERS activate
      neighbor 10.111.11.0 activate
      neighbor 10.112.11.0 activate
      neighbor 10.113.11.0 activate
      network 192.168.255.91/32
   !
   vrf tenant-a
      rd 192.168.255.91:1000
      route-target import evpn 1000:1000
      route-target export evpn 1000:1000
      router-id 192.168.255.91
      redistribute connected
```

## BFD

### Router BFD

#### Router BFD Multihop Summary

| Interval | Minimum RX | Multiplier |
| -------- | ---------- | ---------- |
| 300 | 300 | 3 |

#### Router BFD Device Configuration

```eos
!
router bfd
   multihop interval 300 min-rx 300 multiplier 3
```

## MPLS

### MPLS and LDP

#### MPLS and LDP Summary

| Setting | Value |
| -------- | ---- |
| MPLS IP Enabled | True |
| LDP Enabled | False |
| LDP Router ID | - |
| LDP Interface Disabled Default | - |
| LDP Transport-Address Interface | - |

#### MPLS and LDP Device Configuration

```eos
!
mpls ip
```

### MPLS Interfaces

| Interface | MPLS IP Enabled | LDP Enabled | IGP Sync |
| --------- | --------------- | ----------- | -------- |
| Ethernet1 | True | - | - |
| Ethernet4 | True | - | - |
| Ethernet5 | True | - | - |

## Multicast

### IP IGMP Snooping

#### IP IGMP Snooping Summary

| IGMP Snooping | Fast Leave | Interface Restart Query | Proxy | Restart Query Interval | Robustness Variable |
| ------------- | ---------- | ----------------------- | ----- | ---------------------- | ------------------- |
| Enabled | - | - | - | - | - |

#### IP IGMP Snooping Device Configuration

```eos
```

## Filters

### Route-maps

#### Route-maps Summary

##### RM-EVPN-SOO-IN

| Sequence | Type | Match | Set | Sub-Route-Map | Continue |
| -------- | ---- | ----- | --- | ------------- | -------- |
| 10 | deny | extcommunity ECL-EVPN-SOO | - | - | - |
| 20 | permit | - | - | - | - |

##### RM-EVPN-SOO-OUT

| Sequence | Type | Match | Set | Sub-Route-Map | Continue |
| -------- | ---- | ----- | --- | ------------- | -------- |
| 10 | permit | - | extcommunity soo 10.255.1.91:1 additive | - | - |

#### Route-maps Device Configuration

```eos
!
route-map RM-EVPN-SOO-IN deny 10
   match extcommunity ECL-EVPN-SOO
!
route-map RM-EVPN-SOO-IN permit 20
!
route-map RM-EVPN-SOO-OUT permit 10
   set extcommunity soo 10.255.1.91:1 additive
```

### IP Extended Community Lists

#### IP Extended Community Lists Summary

| List Name | Type | Extended Communities |
| --------- | ---- | -------------------- |
| ECL-EVPN-SOO | permit | soo 10.255.1.91:1 |

#### IP Extended Community Lists Device Configuration

```eos
!
ip extcommunity-list ECL-EVPN-SOO permit soo 10.255.1.91:1
```

## VRF Instances

### VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| MGMT | enabled |
| tenant-a | enabled |

### VRF Instances Device Configuration

```eos
!
vrf instance MGMT
!
vrf instance tenant-a
```
