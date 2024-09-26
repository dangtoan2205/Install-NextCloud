# Install-NextCloud

## 1. Install Ubuntu Server

## 2. Install Nextcloud
```
sudo snap install nextcloud
sudo nextcloud.manual-install netvn password
sudo nextcloud.occ config:system:set trusted_domains 1 --value=*
sudo nextcloud.enable-https self-signed
sudo ufw allow 80,443/tcp
```
## 3. Install ONLYOFFICE Document Server and integrate on NextCloud.
Step 1: Install ONLYOFFICE Document Server on Ubuntu

 - Install PostgreSQL from Ubuntu repository </br>
           Command: </br>
           `sudo apt install postgresql`

  - Then create the onlyoffice database. </br>
           Command: </br>
           `sudo -i -u postgres psql -c "CREATE DATABASE onlyoffice;"`

  -  Create the onlyoffice user. </br>
            Command: </br>
            `sudo -i -u postgres psql -c "CREATE USER onlyoffice WITH password 'onlyoffice';"`
    
   -  Grant permission. </br>
            Command: </br>
            `sudo -i -u postgres psql -c "GRANT ALL privileges ON DATABASE onlyoffice TO onlyoffice;"`

   Note: </br>
            Both the username and password must be onlyoffice. </br>

 - Install NodeJS from official repository </br>

 - Add Node.js repostiory. </br>
           Command: </br>
           `curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -`

 - Install Node.js. </br>
           Command: </br>
           `sudo apt install nodejs -y`

 - Install Redis server and Rabbitmq </br>
           Command: </br>
           `sudo apt install redis-server rabbitmq-server`

 - Check their status. </br>
           Command: </br>
           `systemctl status redis-server` </br>
           `systemctl status rabbitmq-server`
          
 -  You should see they are active (running). </br>

 - Install OnlyOffice document server </br>

 - Add OnlyOffice repository </br>
           Command: </br>
           `echo "deb http://download.onlyoffice.com/repo/d... squeeze main" | sudo tee /etc/apt/sources.list.d/onlyoffice.list`

 - Import OnlyOffice public key. </br>
            Command: </br>
            `sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys CB2DE8E5`

 - Update local package index and install OnlyOffice document server. </br>
            Command: </br>
            `sudo apt update` </br>
            `sudo apt install onlyoffice-documentserver`

Note:
    During the installation process, you will be asked to enter PostgreSQL password for onlyoffice. </br>
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

---
Install Nginx for Ubuntu Server
---
```
sudo apt update
sudo apt upgrade
```
Install Nginx
```
sudo apt install nginx
```
Start nginx and status
```
sudo systemctl start nginx
sudo systemctl status nginx
```
Configure Firewall
```
sudo ufw allow 'Nginx Full'
```

```
Tệp cấu hình chính của Nginx nằm ở /etc/nginx/nginx.conf, và các tệp cấu hình cho từng trang web thường nằm trong thư mục /etc/nginx/sites-available/. Bạn có thể tạo một tệp mới để cấu hình cho trang web của mình.
```

```
sudo systemctl restart nginx
```

---
Install Docker for Ubuntu Server
---



# ONLYOFFICE Document Server
-----
## Create file Docker Compose
```
mkdir onlyoffice
cd onlyoffice

docker-compose.yml
```
version: '3'

services:
  onlyoffice-document-server:
    image: onlyoffice/documentserver
    ports:
      - "81:80"  # Chuyển đổi cổng 80 của container sang cổng 81
    environment:
      - JWT_ENABLED=true
      - JWT_SECRET=your_secret_key  # Thay thế bằng một khóa bảo mật
    volumes:
      - onlyoffice_data:/var/lib/onlyoffice/documentserver

volumes:
  onlyoffice_data:
```
## Run Docker Compose
Run ONLYOFFICE Document Server:
```
docker-compose up -d
```
Add code configure
```
server {
    listen 80;
    server_name 192.168.26.10;  # Địa chỉ IP của Nextcloud

    location / {
        proxy_pass http://192.168.26.10:81;  # Chuyển tiếp đến ONLYOFFICE trên cổng 81
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_buffering off;
        proxy_request_buffering off;
    }
}
```

Test Nginx Configuration

```
sudo nginx -t
```

Reload Nginx

```
sudo systemctl reload nginx
```

## Configure Nextcloud
1. Login Nextcloud





























