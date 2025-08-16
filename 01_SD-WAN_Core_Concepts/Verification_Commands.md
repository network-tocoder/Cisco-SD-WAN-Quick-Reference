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
**Verify Control Plane from vManage**

Go to Monitor > Devices > [device].

```
> Control Connections: Equivalent of `show [sdwan] control connections`
> Real Time > BFD Sessions: Equivalent of `show [sdwan] bfd sessions`
> Real Time > IP Routes: Equivalent of `show ip route [vrf *]`
> To verify the data plane from vManage: Go to Monitor > Devices > [device] > 
Go to Monitor > Devices > [device].
```

**Verify Data Plane from vManage**

Go to Monitor > Devices > [device] > Troubleshooting > Ping | Traceroute

**Perfrom remote packet capture from vManage**

```
> vManage > Administration > Settings > Data Stream > Enabled
> Monitor > Devices > [device] > Troubleshooting > Packet Capture

```
