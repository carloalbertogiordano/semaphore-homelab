# Semaphore Ansible Configuration Repo

This repository contains my Semaphore configuration for managing Ansible automation.

---

## Cheatsheet: Managing SSH Keys for Semaphore

### 1. Generate an SSH key for Semaphore
To allow Semaphore to connect to target hosts without requiring a password, you need to generate a dedicated SSH key.
```bash
ssh-keygen -t ed25519 -f ~/.ssh/ansible_key # or rsa with -t rsa
```
### View the public key
To copy the public key to the target host, display it with:
```bash
cat ~/.ssh/ansible_key.pub
```

## Add the public key to the target host
Manually connect to the target host (using password authentication), then:
```bash
nano ~/.ssh/authorized_keys
```
Paste the contents of your public key (`ansible_key.pub`) at the end of the `authorized_keys` file.
Set the correct permissions:
```bash
chmod 600 ~/.ssh/authorized_keys
```
## Test passwordless SSH connection
From the Semaphore server, verify the connection works without a password:
```bash
ssh -i ~/.ssh/ansible_key user@target_host_ip
```
Replace `user` and `target_host_ip` with the appropriate username and IP address.

