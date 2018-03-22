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

## Add ansible-vault password file:
Create a file called `unifi-ansible.vault` with the required vault password.

This enables access to encrypted data in ansible variables.

It is in `.gitignore` to avoid accidentally putting it in source control.

## Define hosts and variables
Add target host to `hosts.yml`, and create a new `host_vars/myhost.yml` file.

Encrypt necessary data using (for example):
```
ansible-vault encrypt_string --vault-id unifi-ansible.vault --stdin-name public_ip
```

Press Control-D twice to end input.

## Create SSH key (for connecting to backup server)

Run this small playbook that only generates an ssh key for the root user.

```
ansible-playbook root-ssh-key.yml -i hosts.yml --vault-id unifi-ansible.vault --extra-vars "target=mytarget"
```

The SSH public key will be displayed.  Manually add it to `authorized_keys` on
the backup server, so backups can run programmatically.

## Configure the server:
 ```
ansible-playbook unifi-controller.yml -i hosts.yml --vault-id unifi-ansible.vault --extra-vars "target=mytarget"
```
