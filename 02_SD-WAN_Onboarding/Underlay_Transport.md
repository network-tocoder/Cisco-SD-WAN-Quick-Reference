# SD-WAN Controllers – Underlay Transport

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
