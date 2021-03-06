osiam-puppet  [![Build Status](https://travis-ci.org/dacrome/osiam-puppet.png?branch=master)](https://travis-ci.org/dacrome/osiam-puppet)
============

This repository conatins the [OSIAM Puppet Manifest](manifests/init.pp).

The [manifest](manifests/init.pp) currently deploys the OSIAM *osiam-server* war files to an existing application server (tested with Tomcat 7) and initializes the database when `$ensure` is set to "present" or removes the files from their installation directories and cleans the database when `$ensure` is set to "absend". By default this module will install and configure PostgreSQL 9.2 and Tomcat 7.

Prerequisite
============
Host:
* OS: Centos 6, Debian
* maven
* unzip

Usage
============
Use the following example to install everything including PostgreSQL 9.2 and Tomcat 7. This will install OSIAM version <OSIAM-VERSION> and initialize the database 'osiam' on the same maschine. War files will be deployed to `/var/lib/tomcat7/webapps`
```puppet
  class { 'osiam':
        ensure  => present,
        version => '<OSIAM-VERSION>',
  }
```
If you want to manage your database and application server by yourself use this example:
```puppet
  class { 'osiam':
        ensure          => present,
        version         => '<OSIAM-VERSION>',
        installdb       => false,
        dbhost          => '<database_host>',
        dbname          => '<database_name>',
        dbuser          => '<database_user>',
        dbpassword      => '<database_password>',
        installas       => false,
        webappsdir      => '<webapps_directory>',
        owner           => '<application_server_owner>',
        group           => '<application_server_group>',
  }
```

Further usage information can be found in the [manifest's header](manifests/init.pp).
