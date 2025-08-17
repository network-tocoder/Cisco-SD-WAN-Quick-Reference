# Onboarding Internally Hosted Cisco SD-WAN Controllers – Required CLI Config

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
