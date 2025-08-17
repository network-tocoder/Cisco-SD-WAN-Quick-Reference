# Cisco SD-WAN Edge Routers Overview

## Edge Router Variations
- **vEdge Routers** running Viptela OS
  - End-of-Sale Jan 2023, but supported until Jan 2028
- **cEdge Routers** running Cisco IOS XE SD-WAN

## Physical and Virtual Form Factors
- Both vEdge & cEdge Routers come in physical and virtual form factors
  - E.g. vEdge-1000 vs. vEdge Cloud
  - E.g. Cisco ISR 4000 vs. Catalyst 8000v

## Features
- Features are similar between vEdge & cEdge, but different syntax and capabilities

---

## Onboarding Cisco SD-WAN vEdge Routers: Minimum CLI Options

- Host-name
- System-ip (unique, does not need to be routable)
- Site-id (devices in same site don’t form IPsec tunnels with each other)
- Organization-name (must match the ORG in serialFile.viptela)
- vBond IP Address (orchestrator)
- VPN 0 (Transport VPN): interface(s), IP address(es), routing, tunnel color

---

## Example vEdge Router Initial CLI Config

```shell
config
!
system
 host-name vEdge-2
 system-ip 172.17.2.2
 site-id 2
 organization-name VIPTELA.local
 vbond 150.1.1.103
!
vpn 0
 interface ge0/0
  ip address 150.11.1.0/31
  tunnel-interface
   encapsulation ipsec
   color biz-internet
   allow-service all
   no shutdown
  !
 ip route 0.0.0.0/0 150.11.1.1
!
commit and-quit
```

---

## Installing a Private Root CA Certificate on the vEdge Router

If not using Cisco Cloud for PKI, install the Root CA Cert:

```shell
vEdge-2# vshell
vEdge-2:~$ vi MyCA.crt
#   "i" to insert in vi
#   Paste the Root CA Certificate
#   <esc> :wq to save and quit
vEdge-2:~$ exit
vEdge-2# request root-cert-chain install /home/admin/MyCA.crt
```
