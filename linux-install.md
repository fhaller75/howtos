Linux new system config
=======================
###### As used for Linux Mint 18.1 install - 22/01/2017
---

#### Initial system config
* Configure system Update Manager, install packages updates.
* Firefox should be installed by default. Sync and change search engine.
* Add to .bashrc :
```
# Fred Setup
set -o vi
export EDITOR=vi
```
* Automount Windows partitions at boot (required to link to Dropbox folder, for instance):
```shell
# Create mount points:
sudo mkdir -p /mnt/Data /mnt/Backup
# Chech UUID identifiers:
sudo blkid
# Edit fstab
sudo cp -p /etc/fstab /etc/fstab.orig
sudo vi /etc/fstab
```
Add lines similar to the below for NTFS partitions, using above found UUIDs:
```
# Data NTFS - added by fred
UUID=F470354A703514B8  /mnt/Data       ntfs-3g defaults,windows_names,dmask=000,fmask=111 0       0
# Backup NTFS - added by fred
UUID=5CE025B5E0259674  /mnt/Backup     ntfs-3g defaults,windows_names,dmask=000,fmask=111 0       0
```
Reboot
* Increase max file watchers for meteor & dropbox
```shell
sudo vi /etc/sysctl.conf
```
Add at the end:
```
###################################################################
# FHA - Setting for meteor file watcher
# See: https://github.com/meteor/docs/blob/version-NEXT/long-form/file-change-watcher-efficiency.md
fs.inotify.max_user_watches=524288
```
Then restart systemd
```shell
sudo sysctl -p
```

#### Install manually from the web:
* Meteor
```shell
curl https://install.meteor.com/ | sh
```
* VS Code (apt package planned for Jan '17)
Download deb file from https://code.visualstudio.com/Download then:
```shell
sudo dpkg -i <file>.deb
sudo apt-get install -f
```
#### Install from special repositories:
* Grub Customizer, if grub menu needs some fixing following the new install:
```shell
sudo add-apt-repository ppa:danielrichter2007/grub-customizer
sudo apt-get update
sudo apt-get install grub-customizer
```
* Google Chrome:
```shell
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
sudo apt-get update 
sudo apt-get install google-chrome-stable
```
* Dropbox (for Ubuntu 16.04):
```shell
sudo apt-key adv --keyserver pgp.mit.edu --recv-keys 5044912E
sudo sh -c 'echo "deb http://linux.dropbox.com/ubuntu/ xenial main" >> /etc/apt/sources.list.d/dropbox.list'
sudo apt-get update 
sudo apt-get install dropbox python-gpgme
```
* Node v6.x (incl. npm)
```shell
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
```
#### Install apt packages:
```shell
sudo apt-get update 
sudo apt-get install -y \
git \
g++ \
spotify-client \
keepass2 \
hplip-gui \
```
#### Software configuration:
* Git:
Edit $HOME/.gitconfig:
```
[user]
	email = fhaller75@gmail.com
	name = Frédéric Haller
[push]
	default = simple
[credential]
	helper = cache --timeout=7200
```
