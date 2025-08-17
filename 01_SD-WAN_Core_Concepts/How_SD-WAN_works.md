## SD-WAN Operation Flow

#### Step 1: Initial Connection
- vEdge router establishes DTLS tunnel to vBond
- vBond maintains list of authorized device serial numbers (uploaded manually or via Cisco Smart Net)

#### Step 2: Authentication
- Assuming trusted PKI hierarchy (same root certificate)
- vEdge router presents certificate to vBond
- vBond validates certificate and serial number against authorized list
- DTLS connection established upon successful validation

#### Step 3: Controller Notification
- vBond notifies vSmart and vManage about new WAN edge router
- Additional DTLS connections established from vSmart and vManage to new vEdge router

#### Step 4: Configuration Management
- Management tunnel established between vManage and vEdge
- vManage can push configuration templates to new WAN edge securely

#### Step 5: Key Distribution & Route Learning
- vSmart collects IPSec keys for all WAN edge routers
- vSmart learns routes from WAN edges using **OMP (Overlay Management Protocol)**
- Routes and encryption/decryption keys distributed to all WAN edges by default

#### Step 6: Route & Policy Distribution
- vSmart pushes routes and policies to WAN edge routers via OMP
- vSmart functions analogously to a BGP route reflector

#### Step 7: Data Plane Establishment
- WAN edges form IPSec tunnels between sites for data forwarding

#### Step 8: Transport Location Learning
- vSmart learns about **TLOCs (Transport Locations)** from OMP advertisements
- TLOC consists of:
  - WAN router IP towards WAN
  - Additional attributes like color

#### Step 9: Data Plane Security
- IPSec data-plane uses **modified ESP over UDP**
- Provides secure data transmission between sites

#### Step 10: Tunnel Monitoring
- **BFD (Bidirectional Forwarding Detection)** used to track tunnel state
- Monitors both direct and indirect failures
- Ensures high availability and fast failover
