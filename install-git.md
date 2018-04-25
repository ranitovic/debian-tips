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

Go to a directory where existing project will be cloned

```console
git clone git@github.com:mygithubusername/name-of-your-github-project.git
```
