# vagrant_provision

This is an [Ansible](http://www.ansible.com) role to provision a vagrant engine.

## Requirements

- Ansible >= 2.0

## Role Variables

Here is a list of all the default variables for this role, which are also available in `defaults/main.yml`.

```yaml
---
  # List of vagrant boxes needed.
  vagrant_provisioner_boxes: []

  # List of virtual machines (vms) to provision.
  vagrant_provisioner_vms: []

  # Directory inwich will reside vagrantfiles, following the pattern:
  #   virtual_machines/<vm.name>/Vagrantfile
  vagrant_provisioner_vms_directory: ./
  # Created vms inventory file filename
  vagrant_provisioner_inventory_filename: inventory_test
  # Created vms inventory group name
  vagrant_provisioner_vms_group: vagrant_vm
  # Default Ansible Python interpreter
  vagrant_provisioner_default_ansible_python_interpreter: /usr/bin/python2
  # vagrant_provisioner_banner_message: Adds more explicit message (Disabled by default)
  vagrant_provisioner_banner_message:
```

## Dependencies

- vagrant_engine

## Example Playbook

This is an example playbook:

```yaml
---
- name: Create fedora 26 cloud base vagrant instance
  hosts: localhost

  roles:
    role: ansible_vagrant_provisioner
    # vagrant_provisioner_banner_message: Adds more explicit message
    vagrant_provisioner_banner_message: Provision fedora/26-cloud-base virtual machine
    vagrant_provisioner_boxes:
    - name: "fedora/26-cloud-base"
      # state: present or absent (to add remove the box)
      state: present
      # Vagrant provider: libvirt # Only tested with libvirt and docker
      provider: "libvirt"
    vagrant_provisioner_vms:
    - name: "fedora_26_cloud_base"
      # state: present or absent (to add remove the vm)
      state: present
      # DNS name of the vm
      hostname: "fedora-26-cloud-base"
      # Python interpreter (default python2)
      ansible_python_interpreter: /usr/bin/python3
      # subdirectory inside of {{ vagrant_provisioner_vms_directory }}
      subdirectory: "fedora_26_cloud_base"
      # Base Vagrant box
      box:
        name: "fedora/26-cloud-base"
        provider: "libvirt"
      driver: kvm
      memory: 1024
      cpus: 1

---
- name: Delete fedora 26 cloud base vagrant vm instance
  hosts: localhost

  roles:
  - role: ansible_vagrant_provisioner
    vagrant_provisioner_banner_message: Cleanup fedora 26 cloud base virtual machine
    vagrant_provisioner_vms:
    - name: "fedora_26_cloud_base"
      state: absent
      hostname: "fedora-26-cloud-base"
      subdirectory: "fedora_26_cloud_base"

---
- name: Delete fedora 26 cloud base vagrant box
  hosts: localhost

  roles:
  - role: ansible_vagrant_provisioner
    vagrant_provisioner_banner_message: Cleanup fedora 26 cloud base virtual box
    vagrant_provisioner_boxes:
    - name: "fedora/26-cloud-base"
      state: absent
      provider: "libvirt"
```

## Testing

```shell
$ cd ansible_vagrant_provisioner/tests
$ ansible-playbook main.yml
```

## License

GPLv3

## Author Information

- Daniel Sánchez Fábregas ([daniel.sanchez.fabregas@xunta.gal](mailto:daniel.sanchez.fabregas@xunta.gal)). Amtega - Xunta de Galicia
