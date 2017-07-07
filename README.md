# vagrant_provision

This is an [Ansible](http://www.ansible.com) role to provision a vagrant engine.

## Requirements

- Ansible >= 2.0

## Role Variables

Here is a list of all the default variables for this role, which are also available in `defaults/main.yml`.

```yaml
---
TODO
```

## Dependencies

- vagrant_engine

## Example Playbook

This is an example playbook:

```yaml
---

- hosts: all
  roles:
    - vagrant_provisioner TODO
```

## Testing

```shell
$ cd ansible_vagrant_provisioner/test
$ ansible-playbook main.yml
```

## License

GPLv3

## Author Information

- Daniel Sánchez Fábregas ([daniel.sanchez.fabregas@xunta.gal](mailto:daniel.sanchez.fabregas@xunta.gal)). Amtega - Xunta de Galicia
