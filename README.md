# Scotchbox Configuration
My Scripts to work with Vagrant Scotchbox 2.5

## Setup
All commands are designed to be run inside your home folder: `vagrant@scotchbox:~$ `

Run those before starting:

### Bin Setup
```bash
# Creates /home/vagrant/bin directory and exports it to .bashrc
mkdir -p bin;echo "export PATH=$PATH:$HOME/bin" >> .bashrc
```

### Update Ondrej PPA Path
```bash
# Remove outdated PPA for Ondrej-PHP to updated Ondrej/PHP
sudo rm /etc/apt/sources.list.d/ondrej-php*;sudo add-apt-repository ppa:ondrej/php;sudo apt-get update;
```
### Install MySQL 5.6
```bash
# Remove MySql 5.5 and install MySql 5.6
sudo apt-get -y remove mysql-server;sudo apt-get autoremove;sudo apt-get -y install mysql-client-5.6 mysql-client-core-5.6;sudo apt-get -y install mysql-server-5.6
```
### Install PHPMyAdmin
```bash
sudo apt-get install phpmyadmin;sudo chown -R vagrant:vagrant /var/lib/phpmyadmin/tmp/
```
### Install v-add-vhost
```bash
wget https://raw.githubusercontent.com/yahyaerturan/scotchbox_scripts/master/v-add-vhost --output-document=bin/v-add-vhost;chmod +x bin/v-add-vhost
```

### Create a Virtual Host
```bash
v-add-vhost vayes-eys.dev vayesEYS
```
This commands automaticall sets your host path `/home/yahya/Code/vayesEYS/public` as DocumentRoot to your new Virtual Host: `vayes-eys.dev`
