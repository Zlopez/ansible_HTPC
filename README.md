# Ansible script for HTPC
This is a simple ansible script that will setup HTPC machine from Fedora Silverblue machine using Kodi from flatpak.

## Prerequisites
* SSH access to target machine
* Clean Fedora 34 Silverblue installation
* `community.general` collection for flatpak ansible roles. Install it using `ansible-galaxy collection install community.general`

## How to run this playbook
`ansible-playbook -i <target_ip_address>, -u <administrator_user> -k -K htpc-playbook.yml`

`-k` and `-K` is needed to enter the user password for ssh and sudo.

If you don't want automatic updates add `--skip-tags auto-updates`.

### How to start SSH daemon on Silverblue
After installation you will end up in GNOME logged as gnome-initial-setup user.
Create a administrator user which will be used to provision the machine by ansible.

1) Run terminal, press `Super` (key between ALT and CTRL) and type `terminal`
2) Start sshd `systemctl start sshd`
3) Enable sshd `systemctl enable sshd`


### What this script does?
1) Updates Silverblue to latest ostree image
2) Does a reboot to apply new ostree image
3) Creates a new user `htpc`
4) Installs Kodi and VLC from flathub for `htpc` user
5) Update GDM to automatically login as `htpc` user
6) Disable some gnome features - sleep over time, display dim, automatic updates through GNOME Software, Screensaver
7) Creates systemd-timer that is keeping system up to date (Use `--skip tags auto-updates` if you don't want this functionality)
8) Does a reboot (you should be logged in as `htpc` user)
