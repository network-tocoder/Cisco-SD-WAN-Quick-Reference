# Onboarding CLI Config

Onboarding Controllers starts with minimum CLI options:

- **Host-name**
- **System-ip**
  - Does not need to be routable, just a unique Router-ID
- **Site-id**
  - Devices in the same site don’t form IPsec tunnels with each other
- **Organization-name**
  - Must match the ORG in `serialFile.viptela` generated from Cisco Licensing Portal
- **vBond IP Address**
  - Who is the Orchestrator?
- **VPN 0 – The “Transport VPN”**
  - Interface(s), IP address(es), and routing towards the WAN
  - Unique tunnel "color" for each WAN link
    - Color can be used in routing decisions later

---

## Example: Minimum CLI Configuration for vBond Controller

```shell
config t
!
system
 host-name vBond-1
 system-ip 172.17.101.103
 site-id 1
 organization-name VIPTELA.local
 vbond 150.1.1.103 local
!
vpn 0
 interface ge0/0
  ip address 150.1.1.103/24
  tunnel-interface
   encapsulation ipsec
   color biz-internet
   allow-service all
  no shutdown
!
 ip route 0.0.0.0/0 150.1.1.254
!
vpn 512
 interface eth0
  ip dhcp-client
  no shutdown
!
commit and-quit
```
