Git setup tips
==============
###### As used on client site as of 07/03/2017
---

#### Initial global user config:
```bash
git config --global user.name "Frederic Haller"
git config --global user.email "frederic@umea.lu"
git config --global alias.slog 'log --pretty=format:"%h - %cd : %s" --date=short'
git config --global push.default simple
```
#### Define an alias for a short log format:
```bash
git config --global alias.slog 'log --pretty=format:"%h - %cd : %s" --date=short'
```
Usage:
```
# git slog -3
71ee5ec - 2015-11-18 : Scheduler jobs purge: improved logging
```
#### Define an alias to show a commit graph with colored refs:
```bash
git config --global alias.graph 'log --pretty=format:"%C(auto)%h - %cd%d : %s" --date=short --graph'
```
#### Change colors if not readable:
Green on a light term background:
```bash
git config --global color.diff.new 'green bold'
git config --global color.status.updated 'green bold'
git config --global color.branch.current 'green bold'
```
Red on a dark term background:
```bash
git config --global color.status.changed 'red bold'
git config --global color.status.untracked 'red bold'
git config --global color.diff.old 'red bold'
```
#### Pre-commit hook to export type trees:
```bash
#!/usr/bin/bash
#
# Pre-commit hook to call Typetree export if a typetree is part of the commit.
# FHA/Umea - 11/10/2017
#
　
if git rev-parse --verify HEAD >/dev/null 2>&1
then
        against=HEAD
else
        # Initial commit: diff against an empty tree object
        against=4b825dc642cb6eb9a060e54bf8d69288fbee4904
fi
　
for mttfile in $(git diff-index --cached --diff-filter=ACMR --name-only $against | grep "\.mtt$"); do
  noext=${mttfile%.mtt}
  mtsfile=mtx/${noext}.mts
  is_mts_cached=$(git diff-index --cached --diff-filter=ACMR --name-only $against | grep -c ${mtsfile})
  if (( $is_mts_cached == 0 )); then
    compile_V8/texport.bat $mttfile
    git add $mtsfile
  fi
done
exit
```
