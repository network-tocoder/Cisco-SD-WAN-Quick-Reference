

### Understanding IOS XE SD-WAN Mode

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
## Onboarding Cisco SD-WAN cEdge Routers:

### Step#1: IOS XE SD-WAN CEdge Configuration 

> **Tip:** Refer Tunnel config which is the additional config while camparing those vEdge configrations.

```plaintext
config-transaction
 hostname Cat8Kv-1
 system
  system-ip 172.17.101.1
  site-id 101
  organization-name VIPTELA.local
 vbond 150.1.1.103
 !
 interface GigabitEthernet1
  no shutdown
  ip address 10.101.1.1 255.255.255.252
 !
 ip route 0.0.0.0 0.0.0.0 10.101.1.2
 !
 interface Tunnel1
  ip unnumbered GigabitEthernet1
  tunnel source GigabitEthernet1
  tunnel mode sdwan
  no shutdown
 !
 sdwan
  interface GigabitEthernet1
  interface Tunnel1
   encapsulation ipsec
   color biz-internet
   allow-service all
 !
commit
```

### Verification commands

```
show sdwan running-config
```

### Step#2: Installing private Root CA certificate on cEdge

```
copy tftp://192.168.223.127/myca.cert bootflash:
```
```
request platfrom software sdwan root-cert-chain install bootflash:myca.crt
```
