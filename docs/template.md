# LXC Template

Create CT from ubuntu template ```ubuntu-22.04-standard_22.04-1_amd64.tar.zst``` with at least 2G disk size.

### Intall

Remove apparmor
```
apt remove apparmor
```

Install packages
```
apt update
apt upgrade
apt install curl git zsh
```

Install oh-my-zsh
```
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Install docker 
```
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
```

Install docker compose
```
apt install docker-compose
```


### Create Template

Stop container and backup as gzip

Run in pve
```
mv /mnt/<shared>/dump/<backup>.tar.gz /var/lib/vz/template/cache/ubuntu-22.04-standard_22.04-1_amd64-custom.tar.gz
```
