## Make new VM 
### Download Lastest VM Box

### Download Ubuntu 18.04

### Make sure you have a Network Host Network

### Setup VM with 10 GB / 1 CPU Core and  Live CD

### Setup Network on VM
Network #1 -> Host Adapter -> Allow all
Network #2 -> Bridge -> Allow all

### Fix Symlink issue
For MAC users, run this command
```VBoxManage setextradata "VM_Name" VBoxInternal2/SharedFoldersEnableSymlinksCreate/FOLDER_NAME 1```

# Install Ubuntu

## Setup VM
### Install  Guest Tools
```sudo apt-get install virtualbox-guest-x11```
			
### Add a Mount Point via VM UI

### Reboot
```sudo reboot now```

### Check Media
``` ls /media```

### Add user to vbox
```sudo usermod -G vboxsf -a sysadmin```

### Make a new session to see the changes / exit and log back in



## Setup PHP 7.3
### Add PHP 7.3 PPA
```
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
```

### Install PHP 7.3
```sudo apt-get install php7.3```

### Install PHP 7.3 Depenencies for Laravel
```sudo apt-get install php7.3-pgsql php7.3-bcmath php7.3-ctype php7.3-fileinfo php7.3-mbstring php7.3-common php7.3-xml php7.3-tokenizer php7.3-pdo php7.3-zip php7.3-sqlite3 php7.3-gd php7.3-mysql```

### Install Composer
```sudo apt-get install composer```


## Setup Laravel
### Configure Laravel for Global Install
```composer global require laravel/installer```

### Add Laravel to .profile on ubuntu $HOME
```
# set PATH to incude laravel
if [ -d "$HOME/.config/composer/vendor/bin" ] ; then
    PATH="$HOME/.config/composer/vendor/bin:$PATH"
fi
```

### Make a new session to see the changes / exit and log back in

### Create New Project in ~/
```
cd ~/
laravel new www_gbc
```

### Test it
```
cd ~/www_gbc
php artison serve
```

### Test it to your ip
```php artison serve --host 192.168.56.104```


## NodeJS install
### Install nodejs (prep)
```
sudo apt update
sudo apt install build-essential apt-transport-https lsb-release ca-certificates curl
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
```

### Install nodejs
```sudo apt-get install -y nodejs```

### To compile run in the root directory of your laravel project
```npm install && npm run dev```


## Install Postgres
``` sudo apt-get install postgresql ```

### Change Postgres Trust
open the file pg_hba.conf for Ubuntu it will be in `/etc/postgresql/10/main` and change this line:
```
sudo vi /etc/postgresql/10/main/pg_hba.conf
```

```
local   all             postgres                                peer
```
to
```
local   all             postgres                                trust
```
Restart the postgres server

```sudo service postgresql restart```


### Change Postgres Root Password
```
sudo -u postgres psql postgres
```
```
ALTER USER postgres WITH PASSWORD 'new_password!@';
```

### Create Database
```
CREATE DATABASE gbc;
```

### Exit out of Database
```
\q
```

### Run Migrate Script
```php artison migrate```



## Install MySQL Server + PHP My Admin
```sudo apt-get install mysql-server```
```sudo mysql_secure_installation utility```

### Install PHP My Admin
```sudo apt-get install phpmyadmin```

### Allow Remote access
```sudo ufw enable
sudo ufw allow mysql
sudo ufw allow http
sudo ufw allow https
sudo ufw allow ssh
```

### Make new User
```
sudo mysql -p -u root
```

```
CREATE USER 'pmauser'@'localhost' IDENTIFIED BY 'pass@Corona2020';
GRANT ALL PRIVILEGES ON *.* TO 'pmauser'@'localhost' WITH GRANT OPTION;
```
