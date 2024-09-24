# Install-NextCloud

## 1. Install Ubuntu Server

## 2. Install Nextcloud
`sudo snap install nextcloud` </br>
`sudo nextcloud.manual-install netvn password` </br>
`sudo nextcloud.occ config:system:set trusted_domains 1 --value=*` </br>
`sudo nextcloud.enable-https self-signed` </br>
`sudo ufw allow 80,443/tcp` </br>

## 3. Connect Nextcloud from Internet

## 4. 










-----
# Add HDDs
-
`sudo lvresize -l +100%FREE /dev/mapper/ubuntu--vg-ubuntu--lv` </br>
`sudo resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv` </br>
`sudo snap connect nextcloud:removable-media` </br>
------
After running the command above, shut down the Ubuntu Server, connect the new drive, restart the Ubuntu Server, and then run the following code to add the hard drive to the Ubuntu Server.
------
`lsblk` </br>
`sudo fdisk /dev/sdX` </br>
`sudo mkfs.ext4 /dev/sdX1` </br>
`sudo blkid /dev/sdX1` </br>
`sudo mkdir /mnt/disk2` </br>
`sudo nano /etc/fstab` </br>
`PARTUUID=    /mnt/disk2      ext4    defaults        0       0` </br>

`sudo mount /dev/sdX1`


