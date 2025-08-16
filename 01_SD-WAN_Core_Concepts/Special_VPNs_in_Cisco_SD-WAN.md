## Special VPNs in Cisco SD-WAN

**VPN 0 (Transport VPN):**
- Used for underlay connectivity between WAN Edge routers and transport networks (such as MPLS, Internet, LTE).
- All control connections (DTLS/TLS, OMP) and data plane tunnels (IPSec) are established via interfaces in VPN 0.
- No user traffic is routed here; it is strictly for transport and control.

**Note:** This is equivalent to the global routing table on traditional WAN routing.

**VPN 512 (Management VPN):**
- Dedicated for out-of-band management access to WAN Edge routers.
- Used for device management, SSH, SNMP, and communication with vManage for configuration and monitoring.
- Does not participate in data or control plane traffic.

These special VPNs are reserved and required for SD-WAN operation. User-defined VPNs (e.g., VPN 1, 10, etc.) are used for actual data forwarding between sites.
