

## Understanding IOS XE SD-WAN Mode

- Cisco IOS XE routers don't run in SD-WAN Mode by default
- Modes are mutually exclusive; can't run both at the same time
- Enabling SD-WAN mode with `controller-mode enable` requires a reboot
- In SD-WAN mode, router uses `config-transaction` instead of `config t`
- Changes are saved with `commit`

```
controller-mode enable
```