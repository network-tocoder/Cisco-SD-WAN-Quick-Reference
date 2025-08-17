# SD-WAN Onboarding – Key Concepts

This document covers the foundational concepts required for onboarding Cisco SD-WAN controllers and WAN Edge routers, focusing on underlay transport and management VPNs.

## Underlay Transport (VPN 0)

- The first step in onboarding the Controllers is to establish IP transport between themselves & the WAN Edge Routers in the underlay network
  - E.g. over the Internet or MPLS facing link(s)

- Viptela OS uses VPN numbers to represent different routing table spaces
  - VPN numbers in Viptela OS are equivalent to VRFs in Cisco IOS

- VPN 0 is the “Transport VPN”, and is used for links facing towards the WAN
  - VPN 0 is the underlay transport for the overlay IPsec tunnels
    - E.g. towards the public Internet or private MPLS
  - VPN 0 is equivalent to the global (default) VRF in Cisco IOS

- All Controllers & WAN Edge Routers need reachability to each other in VPN 0
  - This is where DTLS tunnels are established for the control-plane

## Management VPN (VPN 512)

- **VPN 512 is the “Management VPN”, used for Out-of-Band Management**
  - VPN 512 is equivalent to VRF “Mgmt-intf” in Cisco IOS
  - Can have a default route separate from the Transport VPN (0)

- **Controllers & Edges don’t need VPN 512 if you only want to manage them in-band**
  - `allow-service` command under the “tunnel-interface” in VPN 0 needs to be modified to allow for in-band management on the WAN facing links
    - E.g. SSH, NETCONF, HTTPS
  - `allow-service` doesn’t affect mgmt between Controllers or to WAN Edge Router
    - DTLS traffic is always allowed in between Controllers and in on WAN Edge
