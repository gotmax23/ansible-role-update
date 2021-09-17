# Ansible Role: update
[![MIT Licensed][badge-license]][link-license]
[![Role gotmax23.update][badge-role]][link-galaxy]
[![Role Version][badge-version]][link-version]
[![Commits since last version][badge-commits-since]][link-version]
[![Galaxy Role Quality][badge-quality]][link-galaxy]
[![Galaxy Role Downloads][badge-downloads]][link-galaxy]
[![Github Actions Molecule workflow status][badge-molecule-workflow]][link-molecule-workflow]
[![Github Actions Galaxy workflow status][badge-galaxy-workflow]][link-galaxy-workflow]

Ansible role that checks for and optionally installs system updates. It also has to the option to print upgradeable packages without actually upgrading them.

## Requirements

For right now, I only test this role using the latest release of the `ansible` pip package, which includes all the collections that are no longer part of `ansible-core`. This is the supported method. However, if you choose to use `ansible-core` or still use Ansible 2.9, you must manually install the following collections:
- community.general

## Role Variables

Here are this role's variables and their default values, as set in [`defaults/main.yml`][link-defaults]. If you'd like, you may change them to customize this role's behavior.

``` yaml
---
# defaults file for update

# Options:
# - `check` to print upgradeable packages without upgrading them
# - `full` to print upgradeable packages and then upgrade them
# - `run` to update all packages without listing them first
mode: full

# This option sets the apt upgrade type. Available options are `dist`, `full`, `safe`, and `true`.
# See the [ansible.builtin.apt][1] module documentation for more information.
update_apt_upgrade_type: true

# This options sets the state key for the zypper module.
# Choose `latest` for a regular upgrade or `dist-upgrade` for the equivalent for `zypper dup`.
# See the [community.general.zypper][2] module documentation for more information.
update_zypper_state: latest

# This option dictates whether zypper should allow a vendor change
update_zypper_allow_vendor_change: false

# Whether to autoremove unneeded dependencies. This only applies to dnf, yum, and apt
update_autoremove: false

```

\[1]: https://docs.ansible.com/ansible/latest/collections/ansible/builtin/apt_module.html

\[2]: https://docs.ansible.com/ansible/latest/collections/community/general/zypper_module.html


## Example Playbook
``` yaml
---
- name: Converge
  hosts: all
  become: true
  tasks:
    - name: "Include update"
      ansible.builtin.include_role:
        name: gotmax23.update

```

## Compatibility
This role is compatible with the following distros:
|distro|versions|
|------|--------|
|Archlinux|any|
|Debian|buster, bullseye|
|EL|7, 8|
|Fedora|33, 34, 35|
|opensuse|15.2, 15.3, tumbleweed|
|Ubuntu|bionic, focal, hirsute|

## License
[MIT][link-license]

## Author
Maxwell G (@gotmax23)

[badge-license]: https://img.shields.io/github/license/gotmax23/ansible-role-update.svg
[link-license]: https://github.com/gotmax23/ansible-role-update/blob/main/LICENSE
[badge-role]: https://img.shields.io/ansible/role/55837.svg
[link-galaxy]: https://galaxy.ansible.com/gotmax23/update
[badge-version]: https://img.shields.io/github/release/gotmax23/ansible-role-update.svg
[link-version]: https://github.com/gotmax23/ansible-role-update/releases/latest
[badge-commits-since]: https://img.shields.io/github/commits-since/gotmax23/ansible-role-update/latest.svg
[badge-quality]: https://img.shields.io/ansible/quality/55837.svg
[badge-downloads]: https://img.shields.io/ansible/role/d/55837.svg
[badge-molecule-workflow]: https://github.com/gotmax23/ansible-role-update/actions/workflows/molecule.yml/badge.svg?branch=main
[link-molecule-workflow]: https://github.com/gotmax23/ansible-role-update/actions/workflows/molecule.yml
[badge-galaxy-workflow]: https://github.com/gotmax23/ansible-role-update/actions/workflows/galaxy.yml/badge.svg
[link-galaxy-workflow]: https://github.com/gotmax23/ansible-role-update/actions/workflows/galaxy.yml
[link-defaults]: https://github.com/gotmax23/ansible-role-update/blob/main/defaults/main.yml
