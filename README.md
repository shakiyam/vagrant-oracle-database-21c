vagrant-oracle-database-21c
===========================

Vagrant + Oracle Linux 7 + Oracle Database 21c (21.3) | Simple setup of a single instance database.

Download
--------

Download Oracle Database 21c (21.3) software from [Oracle Database Software Downloads](https://www.oracle.com/database/technologies/oracle-database-software-downloads.html) and place it in the same directory as the Vagrantfile.

* LINUX.X64_213000_db_home.zip

Set environment variables
-------------------------

Copy the file `dotenv.sample` to a file named `.env` and rewrite the contents as needed.

```shell
ORACLE_BASE=/u01/app/oracle
ORACLE_CHARACTERSET=AL32UTF8
ORACLE_EDITION=EE
ORACLE_HOME=/u01/app/oracle/product/21.0.0/dbhome_1
ORACLE_PASSWORD=oracle
ORACLE_PDB=pdb1
ORACLE_SID=orcl
```

Vagrant configuration
---------------------

If you need to use a proxy, install vagrant-proxyconf and set environment variables for vagrant-proxyconf.

### If your host is macOS or Linux ###

```console
export http_proxy=http://proxy.example.com:80
export https_proxy=http://proxy.example.com:80
vagrant plugin install vagrant-proxyconf

export VAGRANT_HTTP_PROXY=http://proxy.example.com:80
export VAGRANT_HTTPS_PROXY=http://proxy.example.com:80
export VAGRANT_FTP_PROXY=http://proxy.example.com:80
export VAGRANT_NO_PROXY=localhost,127.0.0.1
```

### If your host is Windows ###

```console
SET http_proxy=http://proxy.example.com:80
SET https_proxy=http://proxy.example.com:80
vagrant plugin install vagrant-proxyconf

SET VAGRANT_HTTP_PROXY=http://proxy.example.com:80
SET VAGRANT_HTTPS_PROXY=http://proxy.example.com:80
SET VAGRANT_FTP_PROXY=http://proxy.example.com:80
SET VAGRANT_NO_PROXY=localhost,127.0.0.1
```

Vagrant up
----------

When you run `vagrant up`, the following will work internally.

* Download and boot Oracle Linux 7
* Install Oracle Preinstallation RPM
* Create directories
* Set environment variables
* Set password for oracle user
* Install Oracle Database
* Create a listener
* Create a database

```console
vagrant up
```

Example of use
--------------

Connect to the guest OS.

```console
vagrant ssh
```

Connect to CDB root and confirm the connection.

```console
sudo su - oracle
sqlplus system/oracle
SHOW CON_NAME
```

Connect to PDB, and confirm the connection.

```console
sqlplus system/oracle@localhost/pdb1
SHOW CON_NAME
```

Author
------

[Shinichi Akiyama](https://github.com/shakiyam)

License
-------

[MIT License](https://opensource.org/licenses/MIT)
