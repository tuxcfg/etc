etc directory files
===================


## Installation ##

> **Note:** all existing files will be overwritten!

Init an empty repository, link it with the existing repository, get metadata, force checkout and set the upstream branch:

```bash
cd /etc
git init
git remote add origin https://github.com/tuxcfg/etc.git
git fetch
git checkout -ft origin/master
```

Separate .git from working tree:

```bash
mkdir -p ~/.config/git
mv /etc/.git ~/.config/git/etc
```


## Update ##

Get metadata from a remote repository, verify the difference and apply:

```bash
git-etc fetch
git-etc diff ..origin/master
git-etc pull
```
