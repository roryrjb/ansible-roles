# ansible-roles

> Various ansible roles for deployment on servers and desktops

[![builds.sr.ht status](https://builds.sr.ht/~roryrjb/ansible-roles.svg)](https://builds.sr.ht/~roryrjb/ansible-roles?)

### "Installation"

Either manually copy what you want or if there are a few things of interest
here then clone this into a directory or add this repo as a submodule of another
repo:

```
$ pwd
your-repo
$ git submodule add https://path.to/this/repo
```

If you are working with this repo as a repo in some context then make sure
Ansible knows that this contains roles. So for example if you are in a directory
where you have some existing roles in a directory called `roles/` and you clone
this repo as `ansible-roles/`, change or add a file called `ansible.cfg` and
include the following:

```
[defaults]
roles_path = ./roles:./ansible-roles
```

### Usage

_The following is a suggestion only, you may have a different way of working
with Ansible and roles, and this is how I do it, therefore it is opinionated._

The roles basically assume you have two variables defined for your hosts,
`release` and `distro` and the filenames of the tasks are named accordingly. So
if you consider the repo as a whole, you can have the following (in your `hosts`):

```
[all]
your_hostnames_here

[all:vars]
release=bionic
distro=ubuntu
```

...and the `ubuntu_bionic.yml` task files will be read. The specific logic
for this is defined in each `main.yml` file. With this setup anything that is
distribution and release specific will be isolated from the generic tasks that
are present in `main.yml` which should run on any distro.

### Caveats

The Arch linux roles assume the presence of an `aur` handler, which isn't
included with Ansible by default. I use [this one](https://github.com/kewlfft/ansible-aur).

The `release` variable for Arch is just assumed to be `rolling`, as there aren't
releases exactly.
