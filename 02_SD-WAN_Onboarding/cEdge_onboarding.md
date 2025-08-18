

## Understanding IOS XE SD-WAN Mode

- Cisco IOS XE routers don't run in SD-WAN Mode by default
- Modes are mutually exclusive; can't run both at the same time
- Enabling SD-WAN mode with `controller-mode enable` requires a reboot
- In SD-WAN mode, router uses `config-transaction` instead of `config t`
- Changes are saved with `commit`

```
Cat8_Site101_WAN_01#controller-mode enable 
Enabling controller mode will erase the nvram filesystem, remove all configuration files, and reload the box! 
Ensure the BOOT variable points to a valid image 
Continue? [confirm]
% Warning: Bootstrap config file needed for Day-0 boot is missing
Do you want to abort? (yes/[no]): yes
Cat8_Site101_WAN_01#reboot
```
