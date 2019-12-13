# Vagrant

## Requirements
* Ansible 2.9
* Red Hat/CentOS 8
* Red Hat/CentOS 7

## Role Description
Configures Vagrant and its providers on a host system.

* Installs Vagrant.
    - Version is dictated by the `vagrant_version` variable.
* Configures Vagrant providers.
    - Libvirt
        * Installs `libvirt` and build dependencies for Vagrant `libvirt`
        plugin.
        * Installs Vagrant `libvirt` plugin for `vagrant_users`.
        * Adds `vagrant_users` to `libvirt` group.
        * Ensures `libvirt` daemon is started.
        * Optionally configures automatic DNS resolution on the host system
        for VMs created by Vagrant. E.g. host `srv1` is created by Vagrant,
        `srv1.{{ vagrant_libvirt_network_domain }}` will resolve to IP address
        assigned to `srv1`.

## Role Variables
|Name|Default Value|Description|
|---|---|---|
|`vagrant_providers`|`['libvirt']`|A list of Vagrant providers to configure. __NOTE__: Only `libvirt` is supported at this time.|
|`vagrant_users`|`[]`|A list of users to perform user-level Vagrant configuration on. __WARNING__: The user must exist prior to including this role.|
|`vagrant_version`|`2.2.6`|The version of Vagrant to install.|
|`vagrant_libvirt_autodns`|`no`|Whether to configure automatic DNS resolution on the host system for VMs created by Vagrant. Leverages `libvirt`, `dnsmasq`, and `NetworkManager` integration.|
|`vagrant_libvirt_network_bridge`|`virbr1`|The network bridge to use for the Vagrant `libvirt` network.|
|`vagrant_libvirt_network_domain`|`vagrant.local`|The network domain for the Vagrant `libvirt` network.|
|`vagrant_libvirt_network_name`|`vagrant-libvirt`|The name of the Vagrant `libvirt` network.|

## Example Playbook
```yml
---
- hosts: localhost
  roles:
    - vagrant
```
