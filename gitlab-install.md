Gitlab install and setup tips
=============================
###### As initially setup on client site on 15/03/2018
---

### Linux system parameters tuning
To minimize swap usage on a 4GB RAM host: 
* virtual memory parameters:
```bash
sudo vi /etc/sysctl.conf
```
Add at the end:
```
# Gitlab recommended settings
vm.swappiness = 7
vm.dirty_ratio = 15
vm.dirty_background_ratio = 5
```
Then restart systemd
```bash
sudo sysctl -p
```

### Gitlab server parameters
* reduce gitlab unicorn workers: 
```bash
sudo vi /etc/gitlab/gitlab.rb
```
Change worker processes:
```bash
unicorn['worker processes'] = 3
```
The default at install is 5. We found it to be too much for 4GB RAM. The minimum is 2.  
Then reconfigure:
```bash
sudo gitlab-ctl reconfigure
```
