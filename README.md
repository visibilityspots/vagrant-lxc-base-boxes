# vagrant-lxc base boxes

This repository contains a set of scripts for creating base boxes for usage with
[vagrant-lxc](https://github.com/fgrehm/vagrant-lxc) 1.0+.

## What distros / versions can I build with this?

* Ubuntu
  - Precise 12.04 x86_64
  - Quantal 12.10 x86_64
  - Raring 13.04 x86_64
  - Saucy 13.10 x86_64
  - Trusty 14.04 x86_64
* Debian
  - Squeeze x86_64
  - Wheezy x86_64
  - Jessie x86_64
  - Sid x86_64
* CentOS
  - 6 x86_64
  - 7 x86_64

## Building the boxes

_In order to build the boxes you need to have the `lxc-download`
template available on your machine. If you don't have one around please
create one based on [this](https://github.com/lxc/lxc/blob/master/templates/lxc-download.in)
and drop it on your lxc templates path (usually `/usr/share/lxc/templates`)._

```sh
git clone https://github.com/fgrehm/vagrant-lxc-base-boxes.git
cd vagrant-lxc-base-boxes
make precise
```

By default no provisioning tools will be included but you can pick the ones
you want by providing some environmental variables. For example:

```sh
PUPPET=1 CHEF=1 SALT=1 BABUSHKA=1 \
make precise
```

Will build a Ubuntu Precise x86_64 box with latest Puppet, Chef, Salt and
Babushka pre-installed.

```sh
ACTIVE_CONTAINER=lxc-container-name \
make own_box
```

Will try to build a vagrant box from an activily running lxc container. Make sure you configured the
container for [vagrant](https://github.com/fgrehm/vagrant-lxc/blob/master/BOXES.md)!

## Pre built base boxes

_**NOTE:** None of the base boxes below have a provisioner pre-installed_

| Distribution | VagrantCloud box |
| ------------ | ---------------- |
| Ubuntu Precise 12.04 x86_64 | [fgrehm/precise64-lxc](https://vagrantcloud.com/fgrehm/precise64-lxc) |
| Ubuntu Trusty 14.04 x86_64 | [fgrehm/trusty64-lxc](https://vagrantcloud.com/fgrehm/trusty64-lxc) |
| Debian Wheezy 7 x86_64 | [fgrehm/wheezy64-lxc](https://vagrantcloud.com/fgrehm/wheezy64-lxc) |

_**NOTE:** the base boxes below have the puppet provisioner pre-installed_

| Distribution | VagrantCloud box |
| ------------ | ---------------- |
| CentOS 6 x86_64 | [visibilityspots/centos-6.x-puppet-3.x](https://atlas.hashicorp.com/visibilityspots/boxes/centos-6.x-puppet-3.x) |
| CentOS 6 x86_64 | [visibilityspots/centos-6.x-puppet-4.x](https://atlas.hashicorp.com/visibilityspots/boxes/centos-6.x-puppet-4.x) |
| CentOS 7 x86_64 | [visibilityspots/centos-7.x-puppet-3.x](https://atlas.hashicorp.com/visibilityspots/boxes/centos-7.x-puppet-3.x) |
| CentOS 7 x86_64 | [visibilityspots/centos-7.x-puppet-4.x](https://atlas.hashicorp.com/visibilityspots/boxes/centos-7.x-puppet-4.x) |


## What makes up for a vagrant-lxc base box?

See [vagrant-lxc/BOXES.md](https://github.com/fgrehm/vagrant-lxc/blob/master/BOXES.md)


## Known issues

* We can't get the NFS client to be installed on the containers used for building
  Ubuntu 13.04 / 13.10 / 14.04 base boxes.
* Puppet can't be installed on Debian Sid
* Salt can't be installed on Ubuntu 13.04
