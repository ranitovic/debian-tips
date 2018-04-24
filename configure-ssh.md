# Configure SSH on the server machine

This part explains how to configure SSH server, create a non-root user and setup the private key.

#### Add a new user

```console
adduser myuser
```

#### Create a key pair
```console
ssh-keygen -t rsa -b 4096 -C me@mysite
```

```diff
- For the SSL certificates, you may use the smaller key size of 2048
```

Generated files: id_rsa, id_rsa.pub

#### Setup public key used for connecting to the server without password

```console
mkdir /home/myuser/.ssh
nano /home/myuser/.ssh/authorized_keys
```

* Paste the public key (without the new line character)
* The public key looks like this: ssh-rsa AAAAB3NzaC1y .... c2EAAAADAQAB/Jwjd me@mysite

#### Set the SSH folder permissions

```console
chown myuser:myuser -R /home/myuser/
chmod 700 /home/myuser/.ssh/
chmod 600 /home/myuser/.ssh/authorized_keys
```

```diff
- Sometimes even 400 (read only by the owner permissions will work), this is as strict as we can get.
- Make sure that file ownership is setup properly.
- If all this is too strict, try: chmod 0755 /home/myuser/.ssh, chmod 0644 /home/myuser/.ssh/*
```

#### Configure the SSH server

```console
nano /etc/ssh/sshd_config
```

* Port 2222
* LoginGraceTime 30
* PermitRootLogin no
* PasswordAuthentication no
* X11Forwarding no
* AllowUsers myuser

```console
systemctl restart ssh
```

Restart the SSH server

```console
tail /var/log/auth.log -n 25
```

Show the SSH server log

***

# Configure SSH on the developer machine

This part explains how to configure the SSH client on the development machine.
We need to implement this on the server as well if we need to use GitHub to update server.

#### Create a SSH config file

```console
mkdir ~/.ssh nano ~/.ssh/config
```

```console
Host mysite
HostName mysite.com
Port 2222
IdentityFile ~/.ssh/mysite_rsa
User myuser

Host github.com
HostName github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/git_rsa
```

# Create git private key file

```console
nano /home/myuser/.ssh/git_rsa
```

* Paste the private key

```console
chmod 600 /home/myuser/.ssh/git_rsa
```

Set permissions for the private key file

***

#### Connect to the remote SSH server

```console
ssh mysite
```

#### Copy a file to the remote SSH server

```console
scp -i ~/.ssh/mysite_rsa *.pdf myremoteuser@mysite.org:
```

#### Copy a file from the remote SSH server
scp -i ~/.ssh/mysite_rsa myremoteuser@mysite.org:/file/to/send /where/to/put
