### Samaba

```
arch: amd64
cores: 1
hostname: samba-server
memory: 256
mp0: /mnt/ext1/share,mp=/share1
net0: name=eth0,bridge=vmbr0,firewall=1,hwaddr=3A:BF:2D:CA:7C:7E,ip=dhcp,type=veth
onboot: 1
ostype: ubuntu
rootfs: local-lvm:vm-106-disk-0,size=2G
startup: order=0
swap: 256
lxc.apparmor.profile: unconfined
```

### Mqtt

```
rch: amd64
cores: 1
hostname: mqtt
memory: 256
mp0: /mnt/ext1/share,mp=/share1
net0: name=eth0,bridge=vmbr0,firewall=1,hwaddr=DE:66:B0:B6:78:AC,ip=dhcp,type=veth
onboot: 1
ostype: ubuntu
rootfs: local-lvm:vm-102-disk-0,size=2G
startup: order=1
swap: 256
lxc.apparmor.profile: unconfined
```

### Duplicati
  
```
arch: amd64
cores: 1
hostname: backup
memory: 512
mp0: /mnt/ext1/share,mp=/share1
net0: name=eth0,bridge=vmbr0,firewall=1,hwaddr=1A:D9:D3:F5:5C:54,ip=dhcp,type=veth
onboot: 1
ostype: ubuntu
rootfs: local-lvm:vm-108-disk-0,size=8G
swap: 512
lxc.apparmor.profile: unconfined
```

### Calendar
  
```
arch: amd64
cores: 1
hostname: calendar
memory: 512
mp0: /mnt/ext1/share,mp=/share1
net0: name=eth0,bridge=vmbr0,firewall=1,hwaddr=8E:2D:87:DB:0F:7B,ip=dhcp,type=veth
onboot: 1
ostype: ubuntu
rootfs: local-lvm:vm-107-disk-0,size=4G
startup: order=10
swap: 512
lxc.apparmor.profile: unconfined
```

Create addon folder (see https://github.com/ckulka/baikal-docker/blob/master/examples/docker-compose.localvolumes.yaml)
```
cd /share/addon
mkdir -p config data/db
chown -R 33:33 config data
cd -
```

### Compreface

```
arch: amd64
cores: 1
hostname: compreface
memory: 2048
mp0: /mnt/ext1/share,mp=/share1
net0: name=eth0,bridge=vmbr0,hwaddr=DA:D2:0A:57:B7:86,ip=dhcp,type=veth
ostype: ubuntu
rootfs: local-lvm:vm-104-disk-0,size=24G
swap: 512
lxc.apparmor.profile: unconfined
```

### Deepstack

```
arch: amd64
cores: 1
hostname: deepstack
memory: 2048
mp0: /mnt/ext1/share,mp=/share1
net0: name=eth0,bridge=vmbr0,firewall=1,hwaddr=CE:08:0E:82:2B:6A,ip=dhcp,type=veth
ostype: ubuntu
rootfs: local-lvm:vm-103-disk-0,size=16G
swap: 512
lxc.apparmor.profile: unconfined
```

### NVR

```
arch: amd64
cores: 1
features: nesting=1
hostname: nvr
memory: 1024
mp0: /mnt/ext1/share,mp=/share1
net0: name=eth0,bridge=vmbr0,hwaddr=16:E6:8F:96:CE:0E,ip=dhcp,type=veth
onboot: 1
ostype: ubuntu
rootfs: local-lvm:vm-105-disk-0,size=16G
startup: order=10
swap: 512
lxc.mount.entry: /dev/bus/usb/002/ dev/bus/usb/002/ none bind,optional,create=dir 0,0
lxc.cgroup2.devices.allow: c 189:* rwm
lxc.apparmor.profile: unconfined
lxc.cgroup2.devices.allow: a
lxc.cap.drop: 
lxc.mount.auto: cgroup:rw
```

Check usb devices
```
lsusb
```

### Home Assistant

```
arch: amd64
cores: 1
hostname: home-assistant
memory: 1024
mp0: /mnt/ext1/share,mp=/share1
net0: name=eth0,bridge=vmbr0,firewall=1,hwaddr=D6:A8:B1:DA:6D:6A,ip=dhcp,type=veth
onboot: 1
ostype: ubuntu
rootfs: local-lvm:vm-109-disk-0,size=8G
swap: 512
lxc.cap.drop: 
lxc.apparmor.profile: unconfined
```

### Grafana

Change owner of grafana volume
```
chown -R 472:472 /share1/grafana 
```

