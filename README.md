DigitalOcean Droplet Auto-Create
=========

This role will check your inventory-file and create and configure hosts in DigitalOcean
if hosts unavailable. If hosts is available - role will link IP addresses
of hosts to inventory hostnames.

Hosts configuring include:
1. Install python for Ansible
2. Create user (for cicd or you)
3. Set SSH-key for created user
4. Configure sudoers for no-password sudo
5. Disable Root SSH access

Requirements
------------

1. You should have a viable DigitalOcean account
2. You should add an API token to your account
3. This Ansible Role requires "do_token" role variable

Role Variables
--------------

You should set your DigitalOcean API token as "do_token" variable.
This value must be secured!

```
# your uniq digital ocean api token (dont store it here - its unsecure)
do_token: []
do_user: "{{ ansible_user_id }}"
do_image: "ubuntu-20-04-x64"
do_region: "FRA1"

# more information about sizes look at "digital_ocean_size_info" ansible module
do_size: s-1vcpu-1gb

# ssh-keys should be described in DigitalOcean ID format
do_sshkeys: []
```

Dependencies
------------

Role depends on viable DigitalOcean account.

Example Playbook
----------------

You should call this role first in playbook, for "all" host group.
You also should to disable gathering facts, becouse you can not gather facts
from unavailable hosts. Role will call "setup" module at the end, so you will
get all facts anyway.

Feel free to describe your hosts and groups in inventory file just like you want.

playbook.yml
```
    - hosts: all
      gather_facts: no
      roles:
         - ansible-role-digitalocean
```
hosts
```
[web]
web01
web02

[db]
db01
```

License
-------

BSD

Author Information
------------------

Konstantin Deepezh, https://t.me/deusops
