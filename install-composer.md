# Install Composer

Execute all commands as a **root** user

#### Download composer setup file

```console
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
```

#### Install composer to /usr/local/bin directory

```console
php composer-setup.php --install-dir=/usr/bin --filename=composer
```

#### Check composer version

```console
composer -V
```

#### update composer

```console
composer self-update
```
