# vagrant_provision

This is an [Ansible](http://www.ansible.com) role to provision a vagrant engine.

## Requirements

- Ansible >= 2.4

## Role Variables

A list of all the default variables for this role is available in `defaults/main.yml`.

## Dependencies

- amtega.vagrant_engine

## Example Playbook

This is an example playbook:

```yaml
---
- name: Create fedora 27 cloud base vagrant instance
  hosts: localhost

  roles:
    role: ansible_vagrant_provisioner
    # vagrant_provisioner_banner_message: Adds more explicit message
    vagrant_provisioner_banner_message: Provision fedora/27-cloud-base virtual machine
    vagrant_provisioner_boxes:
    - name: "fedora/27-cloud-base"
      # state: present or absent (to add remove the box)
      state: present
      # Vagrant provider: libvirt # Only tested with libvirt and docker
      provider: "libvirt"
    vagrant_provisioner_vms:
    - name: "fedora_27_cloud_base"
      # state: present or absent (to add remove the vm)
      state: present
      # DNS name of the vm
      hostname: "fedora-27-cloud-base"
      # Python interpreter (default python2)
      ansible_python_interpreter: /usr/bin/python3
      # subdirectory inside of {{ vagrant_provisioner_vms_directory }}
      subdirectory: "fedora_27_cloud_base"
      # Base Vagrant box
      box:
        name: "fedora/27-cloud-base"
        provider: "libvirt"
      driver: kvm
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

```shell
$ cd ansible_vagrant_provisioner/tests
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

- Daniel Sánchez Fábregas ([daniel.sanchez.fabregas@xunta.gal](mailto:daniel.sanchez.fabregas@xunta.gal)). Amtega - Xunta de Galicia
