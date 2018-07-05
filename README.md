# ansible-arch

ansible-arch is an Ansible playbook heavily inspired by [spark](https://github.com/pigmonkey/spark) to provision and recreate from scratch my archlinunx workstation environment.

## Status
The follow roles are done:

* archcore: performs the basic steps on a freshly archlinux install
    * hostname setting
    * user creation
    * timezone, locale and keymapping configuration
    * pacman configuration, mirror refresh, reflector install and mirror sort
    * basic packages install
* home: populates home with a directories skel
* dotfiles: clones a dotfiles repo by git and install them in the home
* x: installs xorg, video driver, window manager and basic gui utilities
* tools: installs some core gui tools (browser, editor)
* mail: installs neomutt, msmtp, offlineimap, notmuch, lbdb, urlscan
* pim: installs pass, vdirsyncer, khal, todoman
* audio: install alsa-utils, mpd, mpc, ncmpc, soundcloud-dl and create media/audio subdirectories

To come:
* backup
* media
* communication
* sys
* dev

## Install
### Clone
```bash
git clone https://github.com/lgaggini/ansible-arch
```

### Requirements

* Ansible
* Vagrant (otional, to test on a disposable vm)

## Configuration
The configuration of the playbook is done by edit the `group_vars/all` file, you can mainly edit:

* some settings for the archlinux installation customization
* dotfiles git repo location
* packages list to be installed for the various roles
* mail_account (imap and smtp) and cal account

## Usage
### Vagrant playground
```bash
cd ansible-arch
vagrant up
ansible-playbook -i vagrant.inventory playbook.yml
```

Every roles and every steps are tagged, you can perform partially run of playbook [using them](https://docs.ansible.com/ansible/latest/user_guide/playbooks_tags.html).

Main available tags are:

* core
* cli
* gui
* dotfiles
* tools
* mail
* pim
* audio
