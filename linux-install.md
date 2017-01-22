Linux new system config procedure
=================================
###### As used for Linux Mint 18.1 install - 22/01/2017

Configure system Update Manager, install packages updates.
Firefox should be installed by default. Sync and change search engine.

Add to .bashrc :
```
# Fred Setup
set -o vi
```
#### Install manually from the web:
* Meteor
```shell
curl https://install.meteor.com/ | sh
```
* VS Code (apt package planned for Jan 17)
Download from https://code.visualstudio.com/Download then:
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
spotify-client \


