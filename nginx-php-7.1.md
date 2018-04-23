# Install nginx with PHP 7.1 FPM on Debian 9.4

#### Install nginx
```console
apt-get install nginx
```

#### Backup the original configuration file
```console
cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.backup
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default.backup
```

#### Test nginx configuration files
```console
nginx -t
```

#### Restart nginx
```console
systemctl reload nginx
```

## Default HTTP Server
```console
nano /etc/nginx/sites-available/default
```

```nginx
server {
        listen 80 default_server;
        listen [::]:80 default_server;

        root /var/www/html;

        # Add index.php to the list if you are using PHP
        index index.html index.php;

        server_name _;

        location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                try_files $uri $uri/ =404;
        }

        # pass PHP scripts to FastCGI server
        location ~ \.php$ {
                include snippets/fastcgi-php.conf;

                # With php-fpm (or other unix sockets):
                fastcgi_pass unix:/var/run/php/php7.1-fpm.sock;
        }
}
```

## Default HTTPS Server
```console
nano /etc/nginx/sites-available/default
```

```nginx
server {
    listen 80 default_server;
    listen [::]:80 default_server;
    server_name ranitovic.com;
    server_tokens off;
    return 302 https://$server_name$request_uri;
}

server {
    listen 443 ssl default_server;

    ssl_certificate /etc/nginx/ChainedCertificate.pem;
    ssl_certificate_key /etc/nginx/private.key;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers HIGH:!aNULL:!MD5;

    root /var/www/html;

    index index.html index.php;

    server_name ranitovic.com;
    server_tokens off;

    location / {
        # First attempt to serve request as file, then
        # as directory, then fall back to displaying a 404.
        try_files $uri $uri/ =404;
    }

    # pass PHP scripts to FastCGI server
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;

        # With php-fpm (or other unix sockets):
        fastcgi_pass unix:/var/run/php/php7.1-fpm.sock;
    }

    error_page 403 /error403.html;
    location = /error403.html {
        root /var/www/html/error;
        internal;
    }

    error_page 404 /error404.html;
    location = /error404.html {
        root /var/www/html/error;
        internal;
    }
}
```

## Virtual Host Example
```console
nano /etc/nginx/sites-available/marko.ranitovic.com
ln -s /etc/nginx/sites-available/marko.ranitovic.com /etc/nginx/sites-enabled/
```

```nginx
server {
    listen 80;
    listen [::]:80;

    server_name marko.ranitovic.com maki.ranitovic.com;
    server_tokens off;
    return 302 https://$server_name$request_uri;
}

server {
    listen 443 ssl;

    ssl_certificate /etc/nginx/ChainedCertificate.pem;
    ssl_certificate_key /etc/nginx/private.key;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers HIGH:!aNULL:!MD5;

    root /var/www/marko;

    # Add index.php to the list if you are using PHP
    index index.html index.php;

    server_name marko.ranitovic.com maki.ranitovic.com;
    server_tokens off;

    location / {
        # First attempt to serve request as file, then
        # as directory, then fall back to displaying a 404.
        try_files $uri $uri/ =404;
    }

    # pass PHP scripts to FastCGI server
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;

        # With php-fpm (or other unix sockets):
        fastcgi_pass unix:/var/run/php/php7.1-fpm.sock;
    }
}
```

## Update nginx configuration
```console
nano /etc/nginx/nginx.conf
```
 * server_names_hash_bucket_size 64;
 
