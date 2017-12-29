Linux new system config
=======================
###### As used for Linux Mint 18.1 install - 22/01/2017
---

#### Initial system config
* Configure system Update Manager, install packages updates.
* Firefox should be installed by default. Sync and change search engine.
* Add to .bashrc :
```bash
# Fred Setup
set -o vi
export EDITOR=vi

alias ls='ls -CF --color=auto'
alias ll='ls -rtl --color=auto'
alias la='ls -lsa --color=auto'
```
* Automount Windows partitions at boot (required to link to Dropbox folder, for instance):
```bash
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
UUID=F470354A703514B8  /mnt/Data       ntfs-3g defaults,windows_names,dmask=000,fmask=111,uid=1000,gid=1000 0       0
# Backup NTFS - added by fred
UUID=5CE025B5E0259674  /mnt/Backup     ntfs-3g defaults,windows_names,dmask=000,fmask=111,uid=1000,gid=1000 0       0
```
Reboot
* Increase max file watchers for meteor & dropbox
```bash
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
```bash
sudo sysctl -p
```

#### Install manually from the web:
* Meteor
```bash
curl https://install.meteor.com/ | sh
```
* VS Code (apt package planned for Jan '17)
Download deb file from https://code.visualstudio.com/Download then:
```bash
sudo dpkg -i <file>.deb
sudo apt-get install -f
```
#### Install apt packages:
```bash
sudo apt-get update 
sudo apt-get install -y \
git \
g++ \
spotify-client \
keepass2 \
hplip-gui \
os-prober \
```
#### Install from special repositories:
* Grub Customizer, if grub menu needs some fixing following the new install:
```bash
sudo add-apt-repository ppa:danielrichter2007/grub-customizer
sudo apt-get update
sudo apt-get install grub-customizer
```
* Google Chrome:
```bash
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
sudo apt-get update 
sudo apt-get install google-chrome-stable
```
* Dropbox (for Ubuntu 16.04):
```bash
sudo apt-key adv --keyserver pgp.mit.edu --recv-keys 5044912E
sudo sh -c 'echo "deb http://linux.dropbox.com/ubuntu/ xenial main" >> /etc/apt/sources.list.d/dropbox.list'
sudo apt-get update 
sudo apt-get install dropbox python-gpgme
```
* Node v8.x (incl. npm)
```bash
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt-get install -y nodejs
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
#### Multiboot:
In case you need to reconfigure the bootloader, first mount all disks containing bootable partitions, then:
```bash
sudo os-prober
sudo grub-update
```
And use the above installed Grub Customizer tool to rearrange the menu if necessary.