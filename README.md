# Scotchbox Configuration
My Scripts to work with Vagrant Scotchbox 2.5

## Setup
Run those before starting:

### Bin Setup
```bash
# Creates /home/vagrant/bin directory and exports it to .bashrc
~$ mkdir -p bin;echo "export PATH=$PATH:$HOME/bin" >> .bashrc
```

### Update Ondrej PPA Path
```bash
sudo rm /etc/apt/sources.list.d/ondrej-php*;sudo add-apt-repository ppa:ondrej/php;sudo apt-get update;
```
### Install MySQL 5.6
```bash
sudo apt-get -y remove mysql-server;sudo apt-get autoremove;sudo apt-get -y install mysql-client-5.6 mysql-client-core-5.6;sudo apt-get -y install mysql-server-5.6
```
### Install PHPMyAdmin
```bash
sudo apt-get install phpmyadmin;sudo chown -R vagrant:vagrant /var/lib/phpmyadmin/tmp/
```
