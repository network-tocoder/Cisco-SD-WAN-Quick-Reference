## Controllers Architecture

### 1. vManage NMS (Network Management System)  aka, SD-WAN Manager
- **Purpose**: GUI for configuring and managing SD-WAN solution
- **Function**: Centralized management interface
- **Plane**: Management plane controller

### 2. vBond Orchestrator (SD-WAN Validator)
- **Purpose**: Automation engine for onboarding new routers
- **Function**: Runs secure DTLS (TLS over UDP) connections
- **Role**: Initial authentication and orchestration

### 3. vSmart Controllers (SD-WAN Controller)
- **Purpose**: Controls routing and policy decisions
- **Function**: Route distribution and policy enforcement
- **Plane**: Control plane controller
