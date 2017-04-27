etc directory files
===================

## Initial deployment ##

> **Note:** all existing files will be overwritten!

As a `root` init an empty repository, link it with the existing repository, get metadata, force checkout and set the upstream branch:

```bash
cd /etc
git init
git remote add origin https://github.com/tuxcfg/etc.git
git fetch
git checkout -ft origin/master
```

Store metadata on a reliable partition not affected on OS reinstall:

```bash
dir="${XDG_CONFIG_HOME:-$HOME/.config}/tuxcfg"
mkdir -p "$dir" && mv .git "$dir/etc" && ln -s "$dir/etc" .git
```

Add local system files and configs (extend this list with your own configs):

```bash
git add *
git commit -m "add system files"
```


## Update ##

Get metadata from a remote repository, verify the difference and apply:

```bash
cd /etc
git fetch
git diff ..origin/master
git merge
```


## OS post-install deployment ##

Restore git link:

```bash
cd /etc
# before root mount this path does not exist
ln -s "${XDG_CONFIG_HOME:-$HOME/.config}/tuxcfg/etc" .git
# use actual path
git --git-dir="/home/root/.config/tuxcfg/etc" checkout -f
```

Restore correct SSH keys permissions after checkout:

```bash
chmod 600 /etc/ssh/ssh_host_*_key
```

Enable systemd services:

```bash
systemctl enable root.mount
systemctl start root.mount
```
