facterdb
========

[![Build Status](https://img.shields.io/travis/camptocamp/facterdb/master.svg)](https://travis-ci.org/camptocamp/facterdb)
[![Code Climate](https://img.shields.io/codeclimate/github/camptocamp/facterdb.svg)](https://codeclimate.com/github/camptocamp/facterdb)
[![Gem Version](https://img.shields.io/gem/v/facterdb.svg)](https://rubygems.org/gems/facterdb)
[![Gem Downloads](https://img.shields.io/gem/dt/facterdb.svg)](https://rubygems.org/gems/facterdb)
[![Coverage Status](https://img.shields.io/coveralls/camptocamp/facterdb.svg)](https://coveralls.io/r/camptocamp/facterdb?branch=master)

A Gem that contains a lot of facts for a lot of Operating Systems.

# Usage

## CLI

```shell
facterdb 'facterversion=/^2.4\./ and (operatingsystem=Debian and operatingsystemrelease>=7 or operatingsystem=RedHat and operatingsystemrelease=/^7/)'
```

Will return a JSON containing the facts for Debian 7, Debian 8 and RedHat 7 generated by Facter 2.4.

## Ruby

```ruby
require 'facterdb'
FacterDB::get_facts()
```

Returns an Array of Hash containing the whole facts database.

## Filtering by Facter version and fact values

### With an Array filter

```ruby
require 'facterdb'

FacterDB.get_facts([{:osfamily => 'Debian'}])
```

### With an Hash filter

```ruby
require 'facterdb'

FacterDB.get_facts({:osfamily => 'Debian'})
```

### With a String filter

```ruby
require 'facterdb'

FacterDB::get_facts('osfamily=Debian')
```

# Facter versions supported

* 1.6
* 1.7
* 2.0
* 2.1
* 2.2
* 2.3
* 2.4
* 3.0
* 3.1
* 3.3

# Operating Systems supported

* ArchLinux
* CentOS 5
* CentOS 6
* CentOS 7
* Debian 6
* Debian 7
* Debian 8
* Fedora 19
* Fedora 22
* Fedora 23
* FreeBSD 9
* FreeBSD 10
* Gentoo
* OpenBSD 5.7
* OpenBSD 5.8
* OpenBSD 5.9
* OpenSuse 12
* OpenSuse 13
* Oracle 5
* Oracle 6
* Oracle 7
* RedHat 5
* RedHat 6
* RedHat 7
* Scientific 5
* Scientific 6
* Scientific 7
* SLES 11
* Solaris 11
* OSX 10.10
* Ubuntu 10.04
* Ubuntu 12.04
* Ubuntu 14.04
* Ubuntu 14.10
* Ubuntu 15.04
* Ubuntu 15.10
* Ubuntu 16.04
* Windows 2012 r2
* Windows 7

# Add new Operating System support

There is `Vagrantfile` to automagically populate `facts` directory by spawning a new VM and launches a provisioning scripts.

```
$ cd facts
$ vagrant up --provision
```

Create i386 facts from x86_64's ones

```
for file in facts/*/*-x86_64.facts; do cat $file | sed -e 's/x86_64/i386/' -e 's/amd64/i386/' > $(echo $file | sed 's/x86_64/i386/'); done
```
Create RedHat, Scientific, OracleLinux facts from CentOS's ones

```
for file in facts/*/centos-*.facts; do cat $file | sed -e 's/CentOS/RedHat/' > $(echo $file | sed 's/centos/redhat/'); done
for file in facts/*/centos-*.facts; do cat $file | sed -e 's/CentOS/Scientific/' > $(echo $file | sed 's/centos/scientific/'); done
for file in facts/*/centos-*.facts; do cat $file | sed -e 's/CentOS/OracleLinux/' > $(echo $file | sed 's/centos/oraclelinux/'); done
```
