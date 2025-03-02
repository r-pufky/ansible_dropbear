# Dropbear
Dropbear initramfs.

## Requirements
[supported platforms](https://github.com/r-pufky/ansible_dropbear/blob/main/meta/main.yml)

[collections/roles](https://github.com/r-pufky/ansible_dropbear/blob/main/meta/requirements.yml)

## Role Variables
[defaults](https://github.com/r-pufky/ansible_dropbear/tree/main/defaults/main)

### Ports
All ports and protocols have been defined for the role.

[defaults/ports.yml](https://github.com/r-pufky/ansible_dropbear/blob/main/defaults/main/ports.yml)

## Dependencies
Part of the [r_pufky.srv](https://github.com/r-pufky/ansible_collection_srv)
collection.

## Host keys
Dropbear host keys are binary files (and NOT standard OpenSSH keypairs); use
tooling provided by the package to generate key material:

``` bash
dropbearkey -t rsa -s 4096 -f dropbear_rsa_host_key
```

This key should be vault encrypted.

## Example Playbook
Read defaults documentation. May be applied in combination with
`r_pufky.srv.wireguard`.

Configure dropbear to use a custom host key and public key for authentication,
remove all pre-generated keys.

host_vars/dropbear.example.com/vars/dropbear.yml
``` yaml
dropbear_service_host_key_path: 'host_vars/dropbear.example.com/dropbear_rsa_host_key'
dropbear_service_remove_host_keys_enable: true
dropbear_service_public_key: '{{ vault_dropbear_service_public_key }}'
```

Apply the base role
``` yaml
- name: 'Apply base configuration'
  ansible.builtin.include_role:
    name: 'r_pufky.srv.wireguard'
```

## Development
Configure [environment](https://github.com/r-pufky/ansible_collection_srv/blob/main/docs/dev/environment/README.md)

Run all unit tests:
``` bash
molecule test --all
```

## Issues
Create a bug and provide as much information as possible.

Associate pull requests with a submitted bug.

## License
[AGPL-3.0 License](https://www.tldrlegal.com/license/gnu-affero-general-public-license-v3-agpl-3-0)
 [(direct link)](https://github.com/r-pufky/ansible_dropbear/blob/main/LICENSE)

## Author Information
PGP Fingerprint: [466EEC2B67516C7117C85CE3A0BC35D16698BAB9](https://keys.openpgp.org/vks/v1/by-fingerprint/466EEC2B67516C7117C85CE3A0BC35D16698BAB9)
| [github gist](https://gist.github.com/r-pufky/a8df36977c55b5bb20829267c4c49d22)
