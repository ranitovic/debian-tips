Install PHP 7.1 on Debian 9.4

#### Become a root user
```console
su
```

#### Update packages

```console
apt-get update
```

#### Show available PHP 7.1 packages if any

```console
apt-cache search php7.1
```

#### Install PHP

```console
apt install ca-certificates apt-transport-https
wget -q https://packages.sury.org/php/apt.gpg -O- | apt-key add -
echo "deb https://packages.sury.org/php/ stretch main" | tee /etc/apt/sources.list.d/php.list
apt update
apt install php7.1-fpm
```

#### Show installed PHP packages

```console
apt list --installed | grep -i php
```

#### Install some PHP extensions

```console
apt-get -y install php7.1-curl php7.1-gd php7.1-zip php7.1-mbstring php7.1-mcrypt php7.1-mysql php7.1-xml php7.1-json
```

#### Optional security fix and a larger upload file size
Default is already secure for the new PHP versions

```console
nano /etc/php/7.1/fpm/php.ini
```

Search command in nano editor is CTRL + W

 * cgi.fix_pathinfo=0
 * upload_max_filesize = 25M

```console
nano /etc/php/7.1/fpm/pool.d/www.conf
```

 * security.limit_extensions = .php

#### Restart PHP

```console
systemctl restart php7.1-fpm
```

#### Show PHP status

```console
systemctl status php7.1-fpm
```

#### Show PHP version

```console
php -v
```

#### Test PHP

```console
nano /var/www/html/info.php
```

Paste the following PHP code:

```php
<?php
    phpinfo();
?>
```

Open site: http://localhost/info.php
