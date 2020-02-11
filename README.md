# docker-openldap-deewee

Openldap configuration files for running an [ldapserver in a container](https://github.com/viaacode/docker-openldap)
using a backup of existing bdb backendss.
Allows to start a read-only copy of the VIAA ldap directory for datawarehouse reporting purposes.

## Description

The configuration comprises
- the memberof module and overlay
- the VIAA custom schema files (ldapns, pwm and x-be-viaa schema's)
- database backend configuration for prd.viaa.be and hetarchief.be

The configuration is designed to run on a secure host.
Anonymous (without password) read only access is provided to all attributes except those that contain sesnitive data, such
as `userPassword` and `pwmResponseSet`.

## Usage
```bash
$ mkdir ~/ldap
$ cd ~/ldap
$ git clone  https://github.com/viaacode/docker-openldap-deewee.git init
$ mkdir data
```
restore the bdb files in the data/ directory, make sure they are owned by `SlapdUserId` and start the container

```bash
$ docker run -d -v ~/ldap/init/:/docker-entrypoint-init -v ~/ldap/data:/var/lib/ldap openldap:latest
```
