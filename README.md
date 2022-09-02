# Home Assistant

- [Samba](#lxc-samba)

- [Homeassistant](#lxc-home-assistant)
- [Deepstack](#lxc-deepstack)
- [Compreface](#lxc-compreface)
- [NVR](#lxc-nvr)
- [Calendar](#lxc-calendar)
- [Mqtt](#lxc-mqtt)

### LXC Samaba

#### Resources
  
Resource|Size|Proxmox Shell
---|---|---
Boot Order | 0 |
Template | ubuntu-22.04-standard_22.04-1_amd64-custom.tar.gz |
Disk | 2G |
Memory | 512Mb |
Share | ```-mp0 /mnt/ext1/share,mp=/share1``` | ```pct set <ctid> -mp0 /mnt/ext1/share,mp=/share1```
Apparmor | ```lxc.apparmor.profile: unconfined``` | ```vi etc/pve/lxc/\<ctid\>.conf```

## LXC Deepstack

Name|Value
---|---
Boot Order | 10
Github | https://github.com/johnolafenwa/DeepStack
Template | ubuntu-22.04-standard_22.04-1_amd64-custom.tar.gz
Unpriviliged | No
Disk | 16G
Memory | 2G

### Configure

Mount share to container, run in pve
```
pct set <ctid> -mp0 /mnt/ext1/share,mp=/share
```

Add to pve lxc conf (/etc/pve/lxc/\<ctid\>.conf)
```
lxc.apparmor.profile: unconfined
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

First download base image
```
docker pull deepquestai/deepstack-base:cpu-1647248158
```

Start addon
```
docker-compose --profile deepstack up -d
```

## LXC Compreface

Resource|Size
---|---
Boot Order | 10
Github | https://github.com/exadel-inc/CompreFace
Template | ubuntu-22.04-standard_22.04-1_amd64-custom.tar.gz
Unpriviliged | No
Disk | 16G
Memory | 1G

### Configure

Mount share to container, run in pve
```
pct set <ctid> -mp0 /mnt/ext1/share,mp=/share
```

Add to pve lxc conf (/etc/pve/lxc/\<ctid\>.conf)
```
lxc.apparmor.profile: unconfined
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
docker-compose --profile compreface up -d
```

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

## LXC Calendar

### Resources
  
Resource|Size
---|---
Boot Order | 10
Template | ubuntu-22.04-standard_22.04-1_amd64-custom.tar.gz
Disk | 2G
Memory | 512Mb
  
### Configure

Mount share to container, run in pve
```
pct set <ctid> -mp0 /mnt/ext1/share,mp=/share
```

Remove security profile, add to pve lxc conf (/etc/pve/lxc/<ctid>.conf)
```
lxc.apparmor.profile: unconfined
```

### Install

Get addons compose
```
git clone https://github.com/eyalcha/home-assistant-addons.git
```

Create addon folder (see https://github.com/ckulka/baikal-docker/blob/master/examples/docker-compose.localvolumes.yaml)
```
cd /share/addon
mkdir -p config data/db
chown -R 33:33 config data
cd -
```
  
Start addon
```
docker-compose --profile calendar up -d
```

## LXC Mqtt

### Resources
  
Resource|Size
---|---
Boot Order | 1
Template | ubuntu-22.04-standard_22.04-1_amd64-custom.tar.gz
Disk | 2G
Memory | 256Mb
  
### Configure

Mount share to container, run in pve
```
pct set <ctid> -mp0 /mnt/ext1/share,mp=/share
```

Remove security profile, add to pve lxc conf (/etc/pve/lxc/\<ctid\>.conf)
```
lxc.apparmor.profile: unconfined
```

Restart container
```
pct reboot <ctid>
```
