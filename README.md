## Requirements
### stablish shh access with the workstation and hosts OpenSsh installed on workstation and hosts:

- Create an SSH key pair (with passphrase) for the normal user account

```bash
shh-keygen -t ed25519 -C "DefaultKey"
```

- Validate the shh key creation

```bash
ls -a .shh
```

```bash
cat .shh/id_ed25519.pub
```

- Add alias to passphrase to save time

```bash
alias ssha='eval $(ssh-agent) && ssh-add'
```

```bash
ssha
```

- Add it to .bashrc (anywhere) to save the alias

```bash
nano .bashrc
```

- Copy user acout key to each host

```bash
shh-copy-id -i ~/.ssh/id_ed25519.pub ${hostip}
```

- Create SSH key with ansible without passphrase (make sure to change key name to ansible when prompted /home/${username}/.shh/ansible)

```bash
shh-keygen -t ed25519 -C "Ansible"
```

- Copy Ansible key to each host

```bash
shh-copy-id -i ~/.ssh/ansible.pub ${hostip}
```

- SSH with Ansible key from workstation

```bash
shh -i ~/.ssh/ansible ${hostip}
```