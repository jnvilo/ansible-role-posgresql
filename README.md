Ansible Role: PostgreSQL
========================

Rewritten from the ground up to take advantage of the community roles provided already within 
ansible. Previous iterations used a lot of duct tape. Those were removed and a lot of the 
operations can be done using (Community.Postgresql)[https://docs.ansible.com/ansible/latest/collections/community/postgresql/index.html]

Basic Usage: (Sample Playbook)
------------------------------
```
- hosts: pgdg
  become: true
  remote_user: ansible
  gather_facts: yes
  vars:
    #Postgres vars
    postgresql_major_version: 10
    postgresql_minor_version: 10.8-1PGDG.rhel8
    postgresql_pg_hba_conf:
      #create adam user
      - type: "local"
        users: "adam"
        databases: "all"
        method: "trust"
        source: "127.0.0.1/32"
        state: "present"
      #configurate such that all local users use "trust" i.e. no password needed
      - type: "local"
        users: "all"
        databases: "all"
        method: "ident"
        source: "127.0.0.1/32"
        state: "present"
 roles:
    - postgresql
```





## pg_hba.conf

By default pg_hba.conf looks like this:

```

# TYPE  DATABASE        USER            ADDRESS                 METHOD

# "local" is for Unix domain socket connections only
local   all             all                                     peer
# IPv4 local connections:
host    all             all             127.0.0.1/32            ident
# IPv6 local connections:
host    all             all             ::1/128                 ident
# Allow replication connections from localhost, by a user with the
# replication privilege.
local   replication     all                                     peer
host    replication     all             127.0.0.1/32            ident
host    replication     all             ::1/128    

```

But we can control this by setting the 




Development
===========

Postgres can be downloaded from:

https://download.postgresql.org/pub/repos/yum/reporpms/

```
Index of /pub/repos/yum/reporpms/
../
EL-6-i386/                                         01-May-2020 16:33                   -
EL-6-x86_64/                                       01-May-2020 16:33                   -
EL-7-aarch64/                                      30-Nov-2021 00:50                   -
EL-7-ppc64le/                                      30-Nov-2021 00:50                   -
EL-7-x86_64/                                       30-Nov-2021 00:49                   -
EL-8-aarch64/                                      30-Nov-2021 00:51                   -
EL-8-ppc64le/                                      30-Nov-2021 00:50                   -
EL-8-x86_64/                                       30-Nov-2021 00:49                   -
EL-9-x86_64/                                       30-Nov-2021 00:49                   -
F-34-x86_64/                                       01-Oct-2021 14:00                   -
F-35-x86_64/                                       03-Nov-2021 11:03                   -
non-free/                                          17-Nov-2019 01:56                   -





```





A brief description of the role goes here.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
