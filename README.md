Seafile init.d Script
=====================

This repository contains an init.d script for running a single instance of Seafile and Seahub with FastCGI.

Installation
------------
```
cp ./seafile /etc/init.d/seafile
chown root:root /etc/init.d/seafile
chmod 755 /etc/init.d/seafile
```

### Autostart
```
update-rc.d seafile defaults
```

Usage
-----
```
/etc/init.d/seafile {start,stop,restart}
```

Setup of Seafile and dependencies
---------------------------------

These are the steps to install Seafile on a clean Debian system. You probably want to use a different database backend or directory structure. Take this as example setup that works with the init.d script.

```
ARCH="x86-64"
VERSION="4.0.4"
SEAFILE_USER="seafile"

# install dependencies
apt-get update
apt-get install python2.7 python-setuptools python-imaging sqlite3

# add user
adduser --disabled-login --disabled-password --gecos "" "$SEAFILE_USER"
su seafile
cd

# download and setup Seafile
wget https://bitbucket.org/haiwen/seafile/downloads/seafile-server_$VERSION_$ARCH.tar.gz
tar -xzvf seafile-server_$VERSION_$ARCH.tar.gz
cd seafile-server-4.0.4
./setup-seafile.sh
```

TODO
----

 * support multiple instances
 * provide Ansible playbook
