Git setup tips
==============
###### As used on client site as of 07/03/2017
---

#### Initial global user config:
```
git config --global user.name "Frederic Haller"
git config --global user.email "frederic@umea.lu"
git config --global alias.slog 'log --pretty=format:"%h - %cd : %s" --date=short'
git config --global push.default simple
```
#### Define an alias for a short log format:
```
git config --global alias.slog 'log --pretty=format:"%h - %cd : %s" --date=short'
```
Usage:
```
# git slog -3
71ee5ec - 2015-11-18 : Scheduler jobs purge: improved logging
```
#### Change colors if not readable:
Green on a light term background:
```
git config --global color.diff.new 'green bold'
git config --global color.status.updated 'green bold'
git config --global color.branch.current 'green bold'
```
Red on a dark term background:
```
git config --global color.status.changed 'red bold'
git config --global color.status.untracked 'red bold'
git config --global color.diff.old 'red bold'
```
