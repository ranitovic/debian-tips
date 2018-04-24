# Install MySQL Server

By default the "apt install mysql-server" command on Debian installs MariaDB server

#### Install Oracle MySQL

```console
echo -e "deb http://repo.mysql.com/apt/debian/ stretch mysql-5.7\ndeb-src http://repo.mysql.com/apt/debian/ stretch mysql-5.7" > /etc/apt/sources.list.d/mysql.list
wget -O /tmp/RPM-GPG-KEY-mysql https://repo.mysql.com/RPM-GPG-KEY-mysql
apt-key add /tmp/RPM-GPG-KEY-mysql
apt update
apt install mysql-server
```

#### Show MySQL server status

```console
systemctl status mysql
```
