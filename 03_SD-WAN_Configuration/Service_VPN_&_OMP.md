# Summary of Cisco SD-WAN Service VPNs and OMP

Hey there! Here's a quick rundown of the key points about Cisco SD-WAN Service VPNs and the Overlay Management Protocol (OMP) based on the content:

- **OMP Basics**: OMP is like a BGP-style protocol that shares prefixes with cool attributes like VPN Number, Transport Location (TLOC), Color, Site-ID, and Tags. These can later help with smart routing policies like Application Aware Routing (AAR).

- **How OMP Works**: It automatically runs between WAN Edge Routers and the vSmart Controller over DTLS tunnels set up during onboarding. WAN Edge Routers share connected, static, BGP, OSPF, or IS-IS routes into OMP, which then sends them to the vSmart. By default, it redistributes connected routes and OSPF Internal on vEdge (but not cEdge), and vSmart acts like a BGP Route Reflector.

- **No Direct OMP Between Edges**: WAN Edge Routers don’t talk OMP directly with each other—only through vSmart. The vSmart takes the routes, applies path selection rules, and reflects them back to the WAN Edges.

- **Service VPNs Purpose**: These VPNs handle traffic inside IPsec tunnels between SD-WAN sites, like private-to-private traffic, and create a full-mesh connectivity within the same VPN. For example, all VPN 1 sites can chat with each other, but not with VPN 2 sites, and vice versa.

- **VPN Number Encoding**: The Service VPN Number is encoded as an MPLS Label in the custom IPsec header. For vEdge (Viptela OS), VPNs 1-511 are for Service VPNs, with 0 for Transport and 512 for MGMT. For cEdge (IOS XE), it uses VRF numbers, where the global default VRF maps to VPN 0, VRF 1 to VPN 1, VRF 2 to VPN 2, and so on.

- **Data-Plane Action**: When an SD-WAN Edge Router gets a packet in an IPsec tunnel, it uses the MPLS Label to figure out which routing table (VPN/VRF) to look up in.

- **Control-Plane Similarity**: SD-WAN routing is like MPLS L3VPN (BGP VPNv4 AFI). In L3VPN, BGP VPNv4 routes include prefix/len, Route Target (RT), and MPLS Labels. The RT defines which routing table the prefix belongs to, segmenting customer info for multi-tenancy. The BGP-learned MPLS Label is used in data-plane encapsulation, and the receiving Edge Router maps it to the right Service VPN Number.

Pretty neat, huh? Let me know if you want to dive deeper!