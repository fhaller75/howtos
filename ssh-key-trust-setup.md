SSH trusted key authentication setup
====================================
##### SSH password-less authentication initiation procedure:
---
On source host:
```bash
ssh-keygen -t rsa -C "$(whoami)@$(hostname)" -b 4096
```
-> no passphrase

Copy public key to target (Alt.: Use `ssh-copy-id -i`, to test & document):
```bash
scp ~/.ssh/id_rsa.pub <target_user>@<target_host>:~
```
Then authorize on target host:
```bash
cat id_rsa.pub >> .ssh/authorized_keys
rm id_rsa.pub
```

Permissions requirements:
```bash
chmod 0700 $HOME
chmod 0700 $HOME/.ssh
chmod 0600 $HOME/.ssh/authorized_keys
```

Should then work password-less. Use ssh -v if any issue.
