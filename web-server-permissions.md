# Setting up file and directory permissions

We need to make our SSH user part of the www-data group

```console
usermod -a -G www-data myuser
```

#### Apply this after every server update

This example is for a Laravel application hosted in /var/www/html

```console
chown -R myuser:www-data /var/www
chmod -R ug+rwx /var/www/html/storage /var/www/html/bootstrap/cache
find /var/www -type f -exec chmod 644 {} \;
find /var/www -type d -exec chmod 755 {} \;
chgrp -R www-data /var/www/html/storage /var/www/html/bootstrap/cache
chmod -R ug+rwx /var/www/html/storage /var/www/html/bootstrap/cache
```
