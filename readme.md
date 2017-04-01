etc directory files
===================

## Initial deployment ##

> **Note:** all existing files will be overwritten!

Init an empty repository, link it with the existing repository, get metadata, force checkout and set the upstream branch:

```bash
cd /etc
git init
git remote add origin https://github.com/tuxcfg/etc.git
git fetch
git checkout -ft origin/master
```

Separate `.git` from working tree:

```bash
dir="${XDG_CONFIG_HOME:-$HOME/.config}/git"
mkdir -p $dir && mv .git "$dir/etc"
```

Add local system files and configs (extend this list with your own configs):

```bash
git-etc add -f hostname hosts machine-id apt/sources.list.d/*.list ssh/*_key* ssh/ssh_config
git-etc commit -m "add system files"
```


## Update ##

Get metadata from a remote repository, verify the difference and apply:

```bash
git-etc fetch
git-etc diff ..origin/master
git-etc merge
```


## Deploy after system reinstall ##

```bash
git-etc checkout -f
```