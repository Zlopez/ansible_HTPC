# Ansible script for HTPC
This is a simple ansible script that will setup HTPC machine from Fedora Silverblue machine using Kodi from flatpak.

## Prerequisites
* SSH access to target machine
* Clean Fedora 29 Silverblue installation

## How to run this playbook
`ansible-playbook -i <target_ip_address>, htpc-playbook.yml -e 'ansible_python_interpreter=/usr/bin/python3'`

Fedora 29 Silverblue doesn't have python 2. This is the reason why you need to specify python interpreter.
If you don't want automatic updates add `--skip-tags auto-updates`.

### How to start SSH daemon on Silverblue
If you created Silverblue with only root user, you will end up in GNOME logged as gnome-initial-setup user.
To login as root you need to edit GRUB entry:

1) Wait till you enter GRUB and hit `e`
2) Add `3` to line beggining with `linux16`
3) Hit `CTRL + x`

You will end up in terminal and can login as root. To enable SSH daemon just run `systemctl enable sshd`
and reboot the machine.

### What this script does?
1) Updates Silverblue to latest ostree image and installs cron
2) Does a reboot to apply new ostree image
3) Creates a new user `kodi`
4) Installs Kodi from flathub and set it as autostart application for `kodi` user
5) Update GDM to automatically login as `kodi` user
6) Creates cron job that is keeping Silverblue and Kodi up to date
7) Does a reboot (you should end up in Kodi, you still need to go through the initial gnome setup)
