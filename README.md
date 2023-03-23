# Ansible Role: MySql
[![Build](https://github.com/eniocarboni/ec-ansible-mysql-role/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/eniocarboni/ec-ansible-mysql-role/actions/workflows/ci.yml) [![GPL License](https://img.shields.io/badge/license-GPL-blue.svg)](https://www.gnu.org/licenses/) [![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.me/EnioCarboni)

An Ansible Role that install, secure Mariadb or MySql server on Ubuntu and EL (RHEL and derived Linux distributions).

## Role Variables

The available variables are listed below, for all references see `defaults/main.yml`

### mysql\_type

It is used to be able to choose between Mariadb server and MySql.

Possible values: *mariadb* | *mysql*

default: **mariadb**

`mysql_type: mariadb`

### mysql\_root\_password

Set Mysql root password on first install then it will be copied to /root/.my.cnf

If not entered or if empty a random password will be created.

default: **empty password**

`mysql_root_password: ''` 

### force\_root\_password

If **true** force set new *mysql\_root\_password* and secure mysql by delete **test db**, **anonymous users** and **not local root users**.

default: **false**

`force_root_password: false`

### secure\_mysql\_rm\_test\_db

It's a boolean value and if set allow to delete test db on first install.

default: **true**

`secure_mysql_rm_test_db: true`

### secure\_mysql\_rm\_anon\_users

It's a boolean value and if set allow to delete anonymous users on first install.

default: **true**

`secure_mysql_rm_anon_users: true`

### secure\_mysql\_rm\_non\_local\_root

It's a boolean value and if set allow to delete non local root users on first install.

default: **true**

`secure_mysql_rm_non_local_root: true`

### mysql\_db

It's an array of hash value where the keys are:

* name: is the db name to create/delete/check
* collation: is the db collation
* encoding: is teh db encoding
* state: is the state *present* or *absent*

default: **[]**

```
mysql_db:
  - name: mydbtest
    collation: utf8_general_ci
    encoding: utf8
    state: present
```

### mysql\_users

It's an array of hash value where the keys are:

* name: is the user to create/delete/check
* host: is the host where user can connect to
* priv: is the privileges of the user (*'mydbtest.\*:ALL'*)
* password: is the user's password
* state: is the state *present* or *absent*

default: **[]**

```
mysql_users:
  - name: myusertest
    host: localhost
    priv: 'mydbtest.*:ALL'
    password: 'v44Hv67n7J3aLits'
    state: present
```

## Dependencies

No dependencies in particolar

## Example Playbook

Install with:

```
ansible-galaxy install eniocarboni.mysql
```

### Example 1: use default variables

```
---
- hosts: all
  become: true

  roles:
    - eniocarboni.mysql
```

### Example 2: with use of custom variables

```
---
- hosts: all
  become: true

  roles:
    - role: eniocarboni.mysql
      mysql_type: mariadb
      mysql_root_password: "My secure password: unset for use random password"
```

## License

GNU General Public License v3.0, see LICENSE file 

## Author Information

This role was created in 2023 by Enio Carboni
