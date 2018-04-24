# Install and configure Git on Debian 9.4

#### Install Git
```console
apt-get install git
```

#### Configure Git globally
```console
git config --global user.name "MyName"
git config --global user.email "myname@mysite.com"
git config --list
```

***

#### Create a new project

Create an empty project on the GitHub without readme or git ignore files.

Go to directory on developer machine where new project is created
Execute the following commands:

```console
git init
git add .
git commit -m "Initial Commit"
git remote add origin git@github.com:mygithubusername/name-of-your-newly-created-project.git
git push -u origin master
```

***

#### Clone an existing project hosted on the GitHub

Go to directory on developer machine where existing project will be cloned

Execute the following commands using a root user:

```console
rm -rf /var/www/html

chown -R myuser:www-data /var/www
chmod -R 775 /var/www/writable-upload-directory
```

Execute the following commands using a non-root user:

```console
git init
git add .
git commit -m "Initial Commit"
git remote add origin git@github.com:mygithubusername/name-of-your-newly-created-project.git
git push -u origin master
```
