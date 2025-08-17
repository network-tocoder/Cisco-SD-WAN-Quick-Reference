# Verifying SD-WAN Controller Onboarding from CLI

Once PKI Authentication is complete, DTLS tunnels form between all Controllers.
- vManage forms one tunnel per-vCPU to vBond

---

## Example: Verify Control Connections from vManage CLI

```shell
vManage-1# show control connections | exclude vedge | tab
```

<img src="../images/verify_sd-wan_onbaording_cli.png" alt="Verifying SD-WAN Controller Onboarding from CLI" width="400"/>

> **Tip:** All controllers should show active DTLS connections after successful onboarding and certificate installation.
