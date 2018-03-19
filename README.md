# vagrant_provision

This is an [Ansible](http://www.ansible.com) role to provision a vagrant engine.

## Requirements

- [Ansible 2.4+](http://docs.ansible.com/ansible/latest/intro_installation.html)
- [Vagrant 2.0+](https://www.vagrantup.com/). You can use [amtega.vagrant_engine](https://galaxy.ansible.com/amtega/vagrant_engine/) role to setup it.

## Role Variables

A list of all the default variables for this role is available in `defaults/main.yml`.

## Dependencies

None.

## Example Playbook

This is an example playbook:

```yaml
---
- name: Create fedora 27 cloud base vagrant instance
  hosts: localhost

  roles:
    role: ansible_vagrant_provisioner    
    vagrant_provisioner_banner_message: Provision fedora/27-cloud-base vm
    vagrant_provisioner_boxes:
      - name: "fedora_27"
        address: "fedora/27-cloud-base"        
        state: present        
        provider: "libvirt"
    vagrant_provisioner_vms:
      - name: "fedora_27"        
        box: "fedora_27"          
        state: started        
        hostname: "fedora-27-cloud-base"        
        ansible_python_interpreter: /usr/bin/python3        
        memory: 1024
        cpus: 1

---
- name: Delete fedora 27 cloud base vagrant vm instance
  hosts: localhost

  roles:
  - role: ansible_vagrant_provisioner
    vagrant_provisioner_banner_message: Cleanup fedora 27 cloud base virtual machine
    vagrant_provisioner_vms:
      - name: "fedora_27_cloud_base"
        state: absent
        hostname: "fedora-27-cloud-base"
        subdirectory: "fedora_27_cloud_base"

---
- name: Delete fedora 27 cloud base vagrant box
  hosts: localhost

  roles:
  - role: ansible_vagrant_provisioner
    vagrant_provisioner_banner_message: Cleanup fedora 27 cloud base virtual box
    vagrant_provisioner_boxes:
      - name: "fedora/27-cloud-base"
        state: absent
        provider: "libvirt"
```

## Testing

You can run the tests with the following commands:

```shell
$ cd tests
$ ansible-playbook main.yml
```

## License

Copyright (C) 2018 AMTEGA - Xunta de Galicia

This role is free software: you can redistribute it and/or modify
it under the terms of:
GNU General Public License version 3, or (at your option) any later version;
or the European Union Public License, either Version 1.2 or – as soon
they will be approved by the European Commission ­subsequent versions of
the EUPL;

This role is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details or European Union Public License for more details.

## Author Information

- Daniel Sánchez Fábregas.
- Juan Antonio Valiño García.
