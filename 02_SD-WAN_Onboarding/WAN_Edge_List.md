# Understanding the WAN Edge List

## Why the WAN Edge List is Important

- **vBond Orchestrator** needs to know the list of Chassis Numbers & Serial Numbers of the WAN Edge Routers to authenticate & onboard them.
  - Can be done automatically through vManage sync to Cisco Smart Licensing
  - Done manually by uploading the `serialFile.viptela` from Cisco Licensing Portal
    - vManage > Configuration > Devices > Upload WAN Edge List
    - Check the box to "send to controllers" to sync to vBond

## Synchronization Requirements

- vBond must have the WAN Edge List synchronized with vManage
  - WAN Edge List not synced will result in DTLS tunnel failure
    - i.e. onboarding fails if vBond can’t authenticate the WAN Edge Router
  - Can be re-synced from vManage > Configuration > Certificates > WAN Edge List > Send to Controllers
  - Verified with `show orchestrator valid-vedges` from vBond CLI

> **Tip:** Always ensure the WAN Edge List is up to date and synchronized to avoid onboarding failures.
