SSH trusted key authentication setup
====================================
##### SSH password-less authentication initiation procedure:
---
On source host:
```bash
ssh-keygen -t rsa
```
-> no passphrase
```bash
scp ~/.ssh/id_rsa.pub <target_user>@<target_host>:~
```

On target host:
```bash
cat id_rsa.pub >> .ssh/authorized_keys
rm id_rsa.pub
chmod 600 .ssh/authorized_keys
```

Connect one time with password.
Should then work password-less. Use ssh -v if any issue.
