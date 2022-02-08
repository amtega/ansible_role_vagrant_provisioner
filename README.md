# Ansible vagrant_provisioner role

This is an [Ansible](http://www.ansible.com) role to provisione vagrant boxes and virtual machines.

## Role Variables

A list of all the default variables for this role is available in `defaults/main.yml`.

## Example Playbook

This is an example playbook:

```yaml
---
- name: Create fedora 30 cloud base vagrant vm
  hosts: localhost
  roles:
    role: ansible_vagrant_provisioner    
    vars:
      vagrant_provisioner_boxes:
        - name: fedora_30
          address: fedora/30-cloud-base
          state: present        
          provider: virtualbox
      vagrant_provisioner_vms:
        - name: fedora_30
          box: fedora_30
          state: started        
          hostname: fedora-30-cloud-base
          ansible_python_interpreter: /usr/bin/python3        
          memory: 1024
          cpus: 1

- name: Delete fedora 30 cloud base vagrant vm
  hosts: localhost
  roles:
  - role: ansible_vagrant_provisioner
    vars:
      vagrant_provisioner_vms:
        - name: "fedora_30_cloud_base"
          state: absent       

- name: Delete fedora 30 cloud base vagrant box
  hosts: localhost
  roles:
  - role: ansible_vagrant_provisioner    
    vars:
      vagrant_provisioner_boxes:
        - name: fedora/30-cloud-base
          state: absent
          provider: virtualbox
```

## Testing

Tests are based on vagrant virtual machines. You can setup vagrant engine quickly using the playbook `files/setup.yml` available in the role [amtega.vagrant_engine](https://galaxy.ansible.com/amtega/vagrant_engine).

Once you have vagrant, you can run the tests with the following commands:

```shell
$ cd tests
$ ansible-playbook main.yml
```

## License

Copyright (C) 2022 AMTEGA - Xunta de Galicia

This role is free software: you can redistribute it and/or modify it under the terms of:

GNU General Public License version 3, or (at your option) any later version; or the European Union Public License, either Version 1.2 or – as soon they will be approved by the European Commission ­subsequent versions of the EUPL.

This role is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details or European Union Public License for more details.

## Author Information

- Juan Antonio Valiño García.
- Daniel Sánchez Fábregas.
