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
