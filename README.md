### 1. Docker

```
docker pull crops/poky:ubuntu-20.04 
docker run -it --name yocto_rpi -v ~/mm/rpi_yocto_workspace1:/workdir --workdir=/workdir crops/poky:ubuntu-20.04 /bin/bash 
docker start yocto_rpi 
docker exec -it yocto_rpi /bin/bash
#or for root priviledge
docker exec -it --user=root yocto_rpi /bin/bash
```

### 2. Building
```
repo init -u https://github.com/zhalat/manifests.git -b rpi4/scarthgap -m default.xml
repo sync -j$(nproc) 
MACHINE=zh-rpi4 DISTRO=zh-distro source ./demo-custom-setup.sh build
bitbake zh-image

flashihg:
sudo bmaptool copy zh-image-zh-rpi4.rootfs-XXX.wic.bz2 /dev/sdX
or
bzip2 -dkc zh-image-zh-rpi4.rootfs-XXX.wic.bz2 | sudo dd of=/dev/sdX bs=4M status=progress conv=fsync
```