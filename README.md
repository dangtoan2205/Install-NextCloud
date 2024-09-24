# Install-NextCloud

## 1. Install Ubuntu Server

## 2. Install Nextcloud
`sudo snap install nextcloud`
`sudo nextcloud.manual-install netvn password`
`sudo nextcloud.occ config:system:set trusted_domains 1 --value=*`
`sudo nextcloud.enable-https self-signed`
`sudo ufw allow 80,443/tcp`

## 3. Connect Nextcloud from Internet

## 4. 










-----
# Add HDDs
---
`sudo lvresize -l +100%FREE /dev/mapper/ubuntu--vg-ubuntu--lv`
`sudo resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv`
`sudo snap connect nextcloud:removable-media`

`
lsblk
sudo fdisk /dev/sdX
sudo mkfs.ext4 /dev/sdX1
sudo blkid /dev/sdX1
sudo mkdir /mnt/disk2
sudo nano /etc/fstab
PARTUUID=    /mnt/disk2      ext4    defaults        0       0

sudo mount /dev/sdX1
`


