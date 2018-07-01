# unifi-ansible

Ansible code to manage Debian-based Unifi Controllers,
including a server certificate using Let's Encrypt and
nightly offsite backup of the controller's autobackups
using borg backup.

### Generate borg repo passphrase
This server's borg repo will be encrypted with a unique passphrase, for protection from snooping on the backup server.

Create a unique passphrase for this particular server's borg backup repository.

### Initialize repo on backup server
Before backups will work, you must create the repo on the borg backup server.

I'm currently using Rsync.net as my backup provider.

Since this is a critical administrative function, it is not automated.

In case there's a BORG_PASSPHRASE environment variable set,
this explicitly unsets it before running the command using `env -u`.
```
env -u BORG_PASSPHRASE borg init --remote-path=borg1 --encryption=repokey-blake2 user@host:unifi-backups/hostname.borg
```

This will prompt you for a borg repo passphrase.  Enter the one you just created.

The server automation will check that this repo is accessible.

## Manage encrypted variables
Create a file called `~/.ansible/unifi.vault` with the required vault password.

This enables access to encrypted data in ansible variables.

Use `ansible-vault encrypt` and `ansible-vault decrypt` to encrypt and decrypt `_vault.yml` files.

## Define hosts and variables
Add hosts and variables to the `inventories` dir.

## Create SSH key (for connecting to backup server)

Run this small playbook that only generates an ssh key for the root user.

```
ansible-playbook plays/root-ssh-key.yml -i inventories/my_inventory
```

The SSH public key will be displayed.  Manually add it to `authorized_keys` on
the backup server, so backups can run programmatically.

## Configure the server:
 ```
ansible-playbook plays/unifi-controller.yml -i inventories/my_inventory
```
