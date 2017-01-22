Linux new system config procedure
=================================
###### As used for Linux Mint 18.1 install 22/01/2017

Configure system Update Manager, install packages updates.
Firefox should be installed by default. Sync and change search engine.

#### Install manually from the web:
* Meteor

#### Install from special repositories:
* Google Chrome:
```shell
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
sudo apt-get update 
sudo apt-get install google-chrome-stable
```

#### Install apt packages:
```
git
