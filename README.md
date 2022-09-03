# Home Assistant

- [Samba](#lxc-samba)
- [Mqtt](#lxc-mqtt)
- [Homeassistant](#lxc-home-assistant)
- [Deepstack](#lxc-deepstack)
- [Compreface](#lxc-compreface)
- [NVR](#lxc-nvr)
- [Calendar](#lxc-calendar)

### Samaba
  
Resource|Size|Proxmox Shell
---|---|---
Type | LXC | 
Boot Order | 0 |
Template | ubuntu-22.04-standard_22.04-1_amd64-custom.tar.gz |
Disk | 2G |
Memory | 512Mb |
Swap | 
Share | ```-mp0 /mnt/ext1/share,mp=/share1``` | ```pct set <ctid> -mp0 /mnt/ext1/share,mp=/share1```
Apparmor | ```lxc.apparmor.profile: unconfined``` | ```vi etc/pve/lxc/\<ctid\>.conf```

### Mqtt
  
Resource|Size|Proxmox Shell
---|---|---
Type | LXC | 
Boot Order | 1
Template | ubuntu-22.04-standard_22.04-1_amd64-custom.tar.gz
Disk | 2G
Memory | 256Mb
Swap | 
Share | ```-mp0 /mnt/ext1/share,mp=/share1``` | ```pct set <ctid> -mp0 /mnt/ext1/share,mp=/share1```
Apparmor | ```lxc.apparmor.profile: unconfined``` | ```vi etc/pve/lxc/\<ctid\>.conf```

### Duplicati
  
Resource|Size|Proxmox Shell
---|---|---
Type | LXC | 
Boot Order | 10
Template | ubuntu-22.04-standard_22.04-1_amd64-custom.tar.gz
Disk | 8G
Memory | 512Mb
Swap | 512Mb
Share | ```-mp0 /mnt/ext1/share,mp=/share1``` | ```pct set <ctid> -mp0 /mnt/ext1/share,mp=/share1```
Apparmor | ```lxc.apparmor.profile: unconfined``` | ```vi etc/pve/lxc/\<ctid\>.conf```

### Calendar
  
Resource|Size|Proxmox Shell
---|---|---
Type | LXC | 
Boot Order | 10
Template | ubuntu-22.04-standard_22.04-1_amd64-custom.tar.gz
Disk | 2G
Memory | 512Mb
Share | ```-mp0 /mnt/ext1/share,mp=/share1``` | ```pct set <ctid> -mp0 /mnt/ext1/share,mp=/share1```
Apparmor | ```lxc.apparmor.profile: unconfined``` | ```vi etc/pve/lxc/\<ctid\>.conf```

Create addon folder (see https://github.com/ckulka/baikal-docker/blob/master/examples/docker-compose.localvolumes.yaml)
```
cd /share/addon
mkdir -p config data/db
chown -R 33:33 config data
cd -
```

### Compreface

Resource|Size|Proxmox Shell
---|---|---
Type | LXC | 
Boot Order | 10
Github | https://github.com/exadel-inc/CompreFace
Template | ubuntu-22.04-standard_22.04-1_amd64-custom.tar.gz
Unpriviliged | No
Disk | 16G
Memory | 2G
Share | ```-mp0 /mnt/ext1/share,mp=/share1``` | ```pct set <ctid> -mp0 /mnt/ext1/share,mp=/share1```
Apparmor | ```lxc.apparmor.profile: unconfined``` | ```vi etc/pve/lxc/\<ctid\>.conf```

### Deepstack

Resource|Size|Proxmox Shell
---|---|---
Type | LXC | 
Boot Order | 10
Github | https://github.com/johnolafenwa/DeepStack
Template | ubuntu-22.04-standard_22.04-1_amd64-custom.tar.gz
Unpriviliged | No
Disk | 16G
Memory | 2G
Share | ```-mp0 /mnt/ext1/share,mp=/share1``` | ```pct set <ctid> -mp0 /mnt/ext1/share,mp=/share1```
Apparmor | ```lxc.apparmor.profile: unconfined``` | ```vi etc/pve/lxc/\<ctid\>.conf```





## LXC NVR

Resource|Size
---|---
Boot Order | 10 (addon)
Template | ubuntu-22.04-standard_22.04-1_amd64-custom.tar.gz
Unpriviliged | No
Disk | 
Memory |

### Configure

Check usb devices
```
lsusb
```

Add to pve lxc conf (/etc/pve/lxc/\<ctid\>.conf)
```
lxc.mount.entry: /dev/bus/usb/002/ dev/bus/usb/002/ none bind,optional,create=dir 0,0
lxc.cgroup2.devices.allow: c 189:* rwm
lxc.apparmor.profile: unconfined
lxc.cgroup2.devices.allow: a
lxc.cap.drop: 
lxc.mount.auto: cgroup:rw
```
  
Share drive with lxc, run in pve
```
pct set <ctid> -mp0 /mnt/ext1/share,mp=/share
```
  
Restart container
```
pct reboot <ctid>
```

### Install

Get addons compose
```
git clone https://github.com/eyalcha/home-assistant-addons.git
cd home-assistant-addons
```

Start addon
```
docker-compose --profile nvr up -d
```
