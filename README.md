# PCOfficina Netinstaller Collection

This repository contains the `pcofficina.netinstaller` Ansible Collection, designed to simplify the deployment of network installation environments. It configures all necessary services to enable:
- PXE booting of different OSes and tools, via a text based menu, using latest `iPXE`
- Network based installation of latest Linux Mint and Windows 11 OSes
- Network boot of latest Memtest86+ memory testing tools

The collection is designed to be executed on Debin/Ubuntu distros or derived, and has an opinionated approach: while most of the behaviours can be adapted adjusting the variables of the various roles, it is designed with reasonable defaults to produce a ready made configuration,



## Ansible version requirements
- Requires Ansible 2.16 or later

## External requirements

- Linux host with network interfaces that can be dedicated to the installation network
- Root/sudo access to configure network services
- Sufficient disk space to store installation images

## Included content

The collection includes the following roles:

| Role Name | Description |
|-----------|-------------|
| [apt_update_cache](roles/apt_update_cache/README.md) | Prepare apt cache |
| [basepath](roles/basepath/README.md) | Define basepath for netinstaller content |
| [common_vars](roles/common_vars/README.md) | Defines shared variables across roles |
| [debian_only](roles/debian_only/README.md) | Ensure this collection can run only on debian/ubuntu or derived distros |
| [dhcp](roles/dhcp/README.md) | Sets up DHCP server with PXE boot configuration |
| [http](roles/http/README.md) | Configures HTTP server for boot resources |
| [ipxe](roles/ipxe/README.md) | Configures iPXE boot environment |
| [iso_linuxmint](roles/iso_linuxmint/README.md) | Prepares Linux Mint ISO for network installation |
| [iso_win11](roles/iso_win11/README.md) | Prepares Windows 11 ISO for network installation |
| [memtest](roles/memtest/README.md) | Integrates Memtest86+ memory diagnostic tool |
| [network](roles/network/README.md) | Configures network interfaces and settings for the installation LAN |
| [nfs](roles/nfs/README.md) | Configures NFS sharing for Linux installations |
| [router](roles/router/README.md) | Configures routing between installation LAN and external networks |
| [run](roles/run/README.md) | Main orchestrator role that applies all required configurations |
| [samba](roles/samba/README.md) | Sets up Samba sharing for Windows installations |
| [tftp](roles/tftp/README.md) | Sets up TFTP server for network booting |


## Using this collection

### Installation

```bash
ansible-galaxy collection install pcofficina.netinstaller
```

You can also include it in a `requirements.yml` file and install it via `ansible-galaxy collection install -r requirements.yml` using the format:

```yaml
collections:
  - name: pcofficina.netinstaller
```

To upgrade the collection to the latest available version, run the following command:

```bash
ansible-galaxy collection install pcofficina.netinstaller --upgrade
```

You can also install a specific version of the collection, for example, if you need to downgrade when something is broken in the latest version (please report an issue in this repository). Use the following syntax where `X.Y.Z` can be any [available version](https://galaxy.ansible.com/pcofficina/netinstaller):

```bash
ansible-galaxy collection install pcofficina.netinstaller:==X.Y.Z
```

### Required Variables

The following variables must be configured for the collection to function properly:

| Variable | Description | Example |
|----------|-------------|---------|
| `network_lan_interface` | Network interface to be used for the installation LAN | `"enp3s0"` |
| `network_lan_ip` | IP address for the server on the installation network | `"192.168.192.1"` |
| `network_lan_net` | Network address for the installation LAN | `"192.168.192.0"` |
| `network_lan_netmask` | Netmask for the installation network in CIDR notation | `"24"` |
| `dhcp_lan_interface` | Interface for DHCP server (usually same as network_lan_interface) | `"{{ network_lan_interface }}"` |

### Primary Usage Pattern

The recommended way to use this collection is with the following playbook structure:

```yaml
- name: NetInstaller Setup
  hosts: netinstall_server
  vars:
    network_lan_interface: "enp3s0"
    network_lan_ip: "192.168.192.1"
    network_lan_net: "192.168.192.0"
    network_lan_netmask: "24"
    dhcp_lan_interface: "{{ network_lan_interface }}"
  tasks:
    - name: Apply Netserver Collection
      ansible.builtin.include_role:
        name: pcofficina.netinstaller.run
```

This playbook configures the specified network interface for the installation LAN and sets up all required services for network booting and installation.

## Release notes

See the [changelog](https://github.com/ansible-collections/pcofficina.netinstaller/tree/main/CHANGELOG.rst).

## Roadmap

Future versions of this collection will include support for additional operating systems and automated testing frameworks.

## More information

- [Ansible Collection overview](https://github.com/ansible-collections/overview)
- [Ansible User guide](https://docs.ansible.com/ansible/devel/user_guide/index.html)
- [Ansible Developer guide](https://docs.ansible.com/ansible/devel/dev_guide/index.html)
- [Ansible Collections Checklist](https://github.com/ansible-collections/overview/blob/main/collection_requirements.rst)
- [Ansible Community code of conduct](https://docs.ansible.com/ansible/devel/community/code_of_conduct.html)
- [The Bullhorn (the Ansible Contributor newsletter)](https://docs.ansible.com/ansible/devel/community/communication.html#the-bullhorn)
- [News for Maintainers](https://github.com/ansible-collections/news-for-maintainers)

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.
