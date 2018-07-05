# linux-mod.eclass

An attempt to add module-signing support for 3rd party modules in gentoo.

## Installation

- Overlay method (preferred)

Assuming you have your own local overlay, create an `eclass` dir
and place provided linux-mod.eclass there.

Reconfigure default section in repos.conf to look like this

```
[DEFAULT]
main-repo = gentoo
eclass-overrides = nameofyouroverlay
```

- Overwrite method (not recommended)

```sh
wget  -O $(portageq get_repo_path / gentoo)/eclass/linux-mod.eclass https://github.com/gyakovlev/linux-mod.eclass/raw/master/linux-mod.eclass
```

if you use git sync the file will stay until upstream file changes.

if you use rsync, the file will be overwritten every sync.
You may want to use postsync hook to copy it after each sync.

## Usage

- Configure kernel to sign modules and optionally require module signatures.

- add `module-sign` to your USE flags.

- emerge packages that provide kernel modules.

- check that modules are signed
```sh
# strings /lib/modules/4.16.12-gentoo/kernel/drivers/net/wireguard.ko  | tail -1
 ~Module signature appended~
 ```


### More info
https://bugs.gentoo.org/show_bug.cgi?id=447352

https://archives.gentoo.org/gentoo-dev/message/4b15b1c851f379a1f802e2f2895cdfa8
