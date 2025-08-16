# Cisco SD-WAN Quick Reference Guide

## Overview
Cisco SD-WAN is a software-defined networking solution that provides centralized control, policy management, and secure connectivity across distributed networks.

## Controllers Architecture

### 1. vManage NMS (Network Management System)
- **Purpose**: GUI for configuring and managing SD-WAN solution
- **Function**: Centralized management interface
- **Plane**: Management plane controller

### 2. vBond Orchestrator
- **Purpose**: Automation engine for onboarding new routers
- **Function**: Runs secure DTLS (TLS over UDP) connections
- **Role**: Initial authentication and orchestration

### 3. vSmart Controllers
- **Purpose**: Controls routing and policy decisions
- **Function**: Route distribution and policy enforcement
- **Plane**: Control plane controller

## Plane Architecture

| Plane | Managed By | Function |
|-------|------------|----------|
| **Management Plane** | vManage | Configuration, monitoring, and management |
| **Control Plane** | vSmart | Routing decisions and policy distribution |
| **Data Plane** | Local vEdge routers | Actual data forwarding |

## Security & Authentication

### PKI Certificates
- **Controllers**: vBond, vSmart, and vManage use PKI certificates for authentication
- **Encryption**: All control & management-plane traffic sent over DTLS is AES-256 encrypted
- **Data Traffic**: Actual user traffic uses IPSec encryption

### Transport Protocol
- **Base Port**: UDP port 12346
- **NAT Traversal**: Can hop around ports for NAT compatibility

## SD-WAN Operation Flow

### Step 1: Initial Connection
- vEdge router establishes DTLS tunnel to vBond
- vBond maintains list of authorized device serial numbers (uploaded manually or via Cisco Smart Net)

### Step 2: Authentication
- Assuming trusted PKI hierarchy (same root certificate)
- vEdge router presents certificate to vBond
- vBond validates certificate and serial number against authorized list
- DTLS connection established upon successful validation

### Step 3: Controller Notification
- vBond notifies vSmart and vManage about new WAN edge router
- Additional DTLS connections established from vSmart and vManage to new vEdge router

### Step 4: Configuration Management
- Management tunnel established between vManage and vEdge
- vManage can push configuration templates to new WAN edge securely

### Step 5: Key Distribution & Route Learning
- vSmart collects IPSec keys for all WAN edge routers
- vSmart learns routes from WAN edges using **OMP (Overlay Management Protocol)**
- Routes and encryption/decryption keys distributed to all WAN edges by default

### Step 6: Route & Policy Distribution
- vSmart pushes routes and policies to WAN edge routers via OMP
- vSmart functions analogously to a BGP route reflector

### Step 7: Data Plane Establishment
- WAN edges form IPSec tunnels between sites for data forwarding

### Step 8: Transport Location Learning
- vSmart learns about **TLOCs (Transport Locations)** from OMP advertisements
- TLOC consists of:
  - WAN router IP towards WAN
  - Additional attributes like color

### Step 9: Data Plane Security
- IPSec data-plane uses **modified ESP over UDP**
- Provides secure data transmission between sites

### Step 10: Tunnel Monitoring
- **BFD (Bidirectional Forwarding Detection)** used to track tunnel state
- Monitors both direct and indirect failures
- Ensures high availability and fast failover

## Key Protocols

| Protocol | Purpose | Layer |
|----------|---------|-------|
| **DTLS** | Secure control/management communication | Control/Management |
| **OMP** | Overlay routing protocol | Control |
| **IPSec** | Data plane encryption | Data |
| **BFD** | Tunnel state monitoring | Data |
| **ESP over UDP** | Modified encapsulation for data | Data |

## Verification Commands

### Control-Plane & Management-Plane DTLS Tunnels

**vBond:**
```
show orchestrator connections
```

**vManage/vSmart/vEdge:**
```
show control connections
```

**cEdge:**
```
show sdwan control connections
```

### Data-Plane (IPSec) Tunnels

**vEdge:**
```
show bfd sessions
```

**cEdge:**
```
show sdwan bfd sessions
```

### Overlay (VPN) Routing

**vEdge:**
```
show ip route [vpn1]
show ip route <prefix> details
```

**cEdge:**
```
show ip route [vrf1]
show ip route <prefix> details
```

### Cisco SD-WAN GUI Verifications

**View a WAN Edge Router's Running Configuration**
```
vManage GUI > Configuration > Devices > (3 dots) > Running Configurations
```
**SSH to WAN Edge Router**
```
vManage GUI > Monitor > Devices > (3 dots) > SSH Terminal
```
## Quick Troubleshooting Checklist

- [ ] Verify PKI certificate validity
- [ ] Check vBond authorized device list
- [ ] Confirm DTLS connectivity (UDP 12346)
- [ ] Validate OMP adjacencies
- [ ] Monitor BFD tunnel states
- [ ] Verify IPSec tunnel establishment

## Network Ports

| Port | Protocol | Purpose |
|------|----------|---------|
| 12346 | UDP | Base transport port (can vary for NAT) |
| 23456 | TCP | vManage web interface |
| 12346-12446 | UDP | DTLS tunnels |

---

*This guide provides a quick reference for Cisco SD-WAN architecture and operations. For detailed configuration and troubleshooting, refer to official Cisco documentation.*
