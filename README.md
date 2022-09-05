### Calendar
  
Create data folder (see https://github.com/ckulka/baikal-docker/blob/master/examples/docker-compose.localvolumes.yaml)
```
cd /share1/baikal
mkdir -p config data/db
chown -R 33:33 config data
cd -
```

### NVR

Check usb devices
```
lsusb
```

### Grafana

Change owner of grafana volume
```
chown -R 472:472 /share1/grafana 
```

