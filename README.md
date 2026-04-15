# Dropbear
Dropbear initramfs.

## [Requirements][i]
Requires [r_pufky.deb][g] galaxy-ng collection.

See [reference documentation][h] for specific dropbear configurations. GRUB
bootloader required (Debian default).

## Role Variables
Detailed variable use documented in defaults. See usage for role operation.

* [defaults][j] - User configurable options.

* [ports][k] - Ports are **not** managed (defined for external use).

## Usage

### Host Keys
Dropbear host keys are **binary** files (**not** standard OpenSSH keypairs).

``` bash
# Use tooling provided by the package to generate key material.
dropbearkey -t rsa -s 4096 -f dropbear_rsa_host_key
ansible-vault encrypt dropbear_rsa_host_key
```

### Authorized Keys

``` bash
# Use a unique keypair with a unique password.
ssh-keygen -b 4096 -t rsa -f ~/.ssh/dropbear
cp dropbear.pub dropbear_authorized_key
ansible-vault encrypt dropbear_authorized_key
```

### Example Playbooks
May be applied in combination with [r_pufky.deb.wireguard][l].

``` yaml
- name: 'Removes unused host keys, rebuilds initramfs, and updates GRUB.'
  ansible.builtin.include_role:
    name: 'r_pufky.deb.dropbear'
  vars:
    dropbear_cfg_host_key_file:
      'host_vars/dropbear.example.com/dropbear_rsa_host_key'
    dropbear_srv_remove_unused_keys: true
    dropbear_cfg_authorized_key_file:
      'host_vars/dropbear.example.com/dropbear_authorized_keys'
```

## Development
Configure [environment][a].

``` bash
# Run all tests.
molecule test --all
```

### [Releases][b]

  Release | Debian | Ansible | Notes
 ---------|--------|---------|-------
  4.x.x   | 13     | 2.20    | Ansible 2.20, semantic versioning.
  3.x.x   | 13     | 2.18    | Migrate to Debian Trixie.
  2.x.x   | 12     | 2.18    | Use standardized libraries.
  1.x.x   | 12     | 2.18    | Migration from private repository.

## Issues
Create a bug and provide as much information as possible.

Associate pull requests with a submitted bug.

## License
[AGPL-3.0 License][c] | [direct link][f]

## Author Information
PGP: [466EEC2B67516C7117C85CE3A0BC35D16698BAB9][d] | [github gist][e]

[a]: https://r-pufky.github.io/ansible_docs
[b]: https://semver.org/spec/v2.0.0
[c]: https://www.tldrlegal.com/license/gnu-affero-general-public-license-v3-agpl-3-0
[d]: https://keys.openpgp.org/vks/v1/by-fingerprint/466EEC2B67516C7117C85CE3A0BC35D16698BAB9
[e]: https://gist.github.com/r-pufky/a8df36977c55b5bb20829267c4c49d22

[f]: https://github.com/r-pufky/ansible_dropbear/blob/main/LICENSE
[g]: https://github.com/r-pufky/ansible_collection_deb
[h]: https://r-pufky.github.io/docs/network/dropbear
[i]: https://github.com/r-pufky/ansible_dropbear/blob/main/meta/main.yml
[j]: https://github.com/r-pufky/ansible_dropbear/tree/main/defaults/main/main.yml
[k]: https://github.com/r-pufky/ansible_dropbear/blob/main/defaults/main/ports.yml
[l]: https://github.com/r-pufky/ansible_dropbear