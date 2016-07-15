
[![Build Status](https://travis-ci.org/wybczu/ansible-role-sysfs.svg?branch=master)](https://travis-ci.org/wybczu/ansible-role-sysfs)

sysfs
=====

A simple role for managing sysfs settings permanently.

Role Variables
--------------

 * `sysfs_configuration` - a configuration hash for sysfs role
   - `name` - name of the configuration file
   - `priority` - files are loaded in lexicographical order - files with higher
      priority are loaded later
   - `options` - a hash with actual options which should be set
     - `action` - *mode* or *owner* - when not specified the role sets the new
       value for specified attribute
     - `attribute` - name of an attribute, specified as a path without `/sys`
       prefix
     - `value` - a new value for the attribute

Example Playbook
----------------

    - hosts: servers
      roles:
        - role: wybczu.sysctl
          sysfs_configuration:
            name: set_sda_timeout
            priority: 50
            options:
              - { attribute: 'block/sda/device/timeout', value: '60' }
              - { action: 'owner', attribute: 'power/state', value: 'root:power' }
              - { action: 'mode', attribute: 'power/state', value: '0660' }

License
-------

Apache
