# Install Oracle MySQL Server on Debian 9.11

By default the "apt install mysql-server" command on Debian installs MariaDB server

#### Install MySQL

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

#### Re-install MySQL

```console
systemctl stop mysql

apt-get remove -y mysql-*

apt-get purge -y mysql-*

apt install mysql-server
```
