# Install-NextCloud

## 1. Install Ubuntu Server

## 2. Install Nextcloud
`sudo snap install nextcloud` </br>
`sudo nextcloud.manual-install netvn password` </br>
`sudo nextcloud.occ config:system:set trusted_domains 1 --value=*` </br>
`sudo nextcloud.enable-https self-signed` </br>
`sudo ufw allow 80,443/tcp` </br>

## 3. Install ONLYOFFICE Document Server and integrate on NextCloud.
Step 1: Install ONLYOFFICE Document Server on Ubuntu

 - Install PostgreSQL from Ubuntu repository
           Command:
           `sudo apt install postgresql`

  - Then create the onlyoffice database.
           Command:
           `sudo -i -u postgres psql -c "CREATE DATABASE onlyoffice;"`

  -  Create the onlyoffice user.
            Command:
            `sudo -i -u postgres psql -c "CREATE USER onlyoffice WITH password 'onlyoffice';"`
    
   -  Grant permission.
            Command:
            `sudo -i -u postgres psql -c "GRANT ALL privileges ON DATABASE onlyoffice TO onlyoffice;"`

   Note:
            Both the username and password must be onlyoffice.

 - Install NodeJS from official repository

 - Add Node.js repostiory.
           Command:
           `curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -`

 - Install Node.js.
           Command:
           `sudo apt install nodejs -y`

 - Install Redis server and Rabbitmq
           Command:
           `sudo apt install redis-server rabbitmq-server`

 - Check their status.
           Command:
           `systemctl status redis-server`
           `systemctl status rabbitmq-server`

 -  You should see they are active (running).

 - Install OnlyOffice document server

 - Add OnlyOffice repository
           Command:
           `echo "deb http://download.onlyoffice.com/repo/d... squeeze main" | sudo tee /etc/apt/sources.list.d/onlyoffice.list`

 - Import OnlyOffice public key.
            Command:
            `sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys CB2DE8E5`

 - Update local package index and install OnlyOffice document server.
            Command:
            `sudo apt update`
            `sudo apt install onlyoffice-documentserver`

Note:
    During the installation process, you will be asked to enter PostgreSQL password for onlyoffice.
    Enter “onlyoffice” (without double quotes).


-----
# Add HDDs

`sudo lvresize -l +100%FREE /dev/mapper/ubuntu--vg-ubuntu--lv` </br>
`sudo resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv` </br>
`sudo snap connect nextcloud:removable-media` </br>

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


