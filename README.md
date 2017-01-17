# Scotchbox Configuration
My Scripts to work with Vagrant Scotchbox 2.5

There are some standard tasks which I have to do after a new Scotchbox. Changing Ondrej PPA Path, Upgrading MySQL, Installing PHPMyAdmin, tweak php.ini, etc. So I have written some codes to automate it.

Scripts are assuming that you are on a Mac HOST machine.

Minor changes are needed for Ubuntu HOST machines which are also documentated here.

#### First just a little addition to Vagrantfile
```bash
// For Mac
config.vm.synced_folder "/Users/yahyaerturan/Code", "/home/vagrant/Code", :mount_options => ["dmode=777", "fmode=666"]
```

```bash
// For Ubuntu
config.vm.synced_folder "/home/yahya/Code", "/home/vagrant/Code", :mount_options => ["dmode=777", "fmode=666"]
```

## Remimder
All commands are designed to be run inside your home folder: `vagrant@scotchbox:~$ ` or `~$`

## Setting up the HOST Machine
First we must some adjustments in our host machine.

### Download and Run v-setup-host
```bash
wget https://raw.githubusercontent.com/yahyaerturan/scotchbox_scripts/master/v-setup-host --output-document=v-setup-host-machine-for-vagrant;chmod +x v-setup-host-machine-for-vagrant;./v-setup-host-machine-for-vagrant;rm v-setup-host-machine-for-vagrant
```

It checks if you have a `~/Bin` folder first. If not, creates one. Then it downloads `v-add-domain` to your `~/Bin` directory and marks it as executable. Host Machine is ready :)

## Setup GUEST Machine
```bash
wget https://raw.githubusercontent.com/yahyaerturan/scotchbox_scripts/master/v-setup-guest --output-document=v-setup-guest-machine-for-vagrant;chmod +x v-setup-guest-machine-for-vagrant;./v-setup-guest-machine-for-vagrant;rm v-setup-guest-machine-for-vagrant
```

It checks if you have a `~/Bin` folder for first. If not, creates one. Then it downloads `v-add-host` to your `~/Bin` directory and marks it as executable.

Now you can create a new virtual host by:

```bash
v-add-host vayes-eys.dev vayesEYS
```

This commands automaticall sets `/home/vagrant/Code/vayesEYS/public`, which is a reflection of `~/Code/vayesEYS/public` on your _HOST_ machine as the DocumentRoot to your new Virtual Host: `vayes-eys.dev`

`vayesEYS` is the name of the folder under the `~/Code` folder on your HOST machine. It should have a `public` folder to serve.

But script is still running :)

Let's have a look at what it is doing:

#### Update Ondrej PPA Path
```bash
# Replace outdated PPA for Ondrej-PHP to updated Ondrej/PHP
sudo rm /etc/apt/sources.list.d/ondrej-php*;sudo add-apt-repository ppa:ondrej/php;sudo apt-get update;
```
#### Install MySQL 5.6
```bash
# Remove MySql 5.5 and install MySql 5.6
sudo apt-get -y remove mysql-server;sudo apt-get autoremove;sudo apt-get -y install mysql-client-5.6 mysql-client-core-5.6;sudo apt-get -y install mysql-server-5.6
```
#### Install PHPMyAdmin and Change of Owner of its tmp/ folder
```bash
sudo apt-get install phpmyadmin;sudo chown -R vagrant:vagrant /var/lib/phpmyadmin/tmp/
```
#### Update PHP Settings
```bash
# Set Post Max Size
sudo sed -i s,"post_max_size = 8M","post_max_size = 64M",g /etc/php5/apache2/php.ini
# Set Upload Max File Size
sudo sed -i s,"upload_max_filesize = 2M","upload_max_filesize = 64M",g /etc/php5/apache2/php.ini
# Set Date Timezone to Europe/Istanbul
sudo sed -i s,";date.timezone =","date.timezone = \"Europe/Istanbul\"",g /etc/php5/apache2/php.ini
# Enable Short Open Tags
sudo sed -i s,"short_open_tag = Off","short_open_tag = On",g /etc/php5/apache2/php.ini
```

#### Composer SelfUpdate
```bash
sudo composer selfupdate
```


Hope you enjoy it!
