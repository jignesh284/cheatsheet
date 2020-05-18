

### Keygen

```bash
ssh-keygen -t rsa -b 4096

scp ~/.ssh/id_rsa.pub username@192.164.30.20:/path/filename.pub

cat ~/.ssh/filename.pub >> ~/.ssh/authorized_keys

# to all the folder
chmod 700 ~/.ssh

# to all the files
chmod 600 ~/.ssh/*

# genetate backup for ssh config
sudo cp /etc/ssh/sshd_config /etc/ssh/ssh_config.bak

# cange the config file
sudo vim /etc/ssh/sshd_config

# change password authentication to no
PasswordAuthentication no
```

