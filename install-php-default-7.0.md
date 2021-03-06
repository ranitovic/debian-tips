# Default PHP 7.0 Installation on Debian 9.4

#### Become a root user
```console
su
```

#### Update packages

```console
apt-get update
```

#### Show available PHP 7.0 packages if any

```console
apt-cache search php7.0
```

#### Install PHP

```console
apt-get -y install php7.0-fpm
apt update
```

#### Show installed PHP packages

```console
apt list --installed | grep -i php
```

#### Install some PHP extensions

```console
apt-get -y install php7.0-curl php7.0-gd php7.0-zip php7.0-mbstring php7.0-mcrypt php7.0-mysql php7.0-xml php7.0-json
```

#### Optional security fix and a larger upload file size
Default is already secure for the new PHP versions

```console
nano /etc/php/7.0/fpm/php.ini
```

Search command in nano editor is CTRL + W

 * cgi.fix_pathinfo=0
 * upload_max_filesize = 25M

```console
nano /etc/php/7.0/fpm/pool.d/www.conf
```

 * security.limit_extensions = .php

#### Restart PHP

```console
systemctl restart php7.0-fpm
```

#### Show PHP status

```console
systemctl status php7.0-fpm
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
