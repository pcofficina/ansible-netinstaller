# Pcofficina.Netinstaller Run Role

This is the main orchestration role for the PCOfficina Netinstaller collection. It configures a server to provide network installation services by applying all the necessary component roles in the correct sequence.

## Role Purpose

The `run` role:
1. Validates required variables
2. Configures the specified network interface
3. Applies all component roles to set up a complete network installation environment
4. Ensures all services are properly configured and running

## Requirements

- Root/sudo access on the target host
- A dedicated network interface for the installation network
- Sufficient disk space for OS installation files

## Role Variables

### Required Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `network_lan_interface` | Network interface to be used for installation LAN | String | Yes | None |
| `network_lan_ip` | IP address for the server on the installation network | String | Yes | None |
| `network_lan_net` | Network address for the installation LAN | String | Yes | None |
| `network_lan_netmask` | Netmask for the installation network in CIDR notation | String | Yes | None |
| `dhcp_lan_interface` | Interface for DHCP server (usually the same as network_lan_interface) | String | Yes | None |

### Optional Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `netinstaller_data_dir` | Directory to store installation files | String | No | "/opt/netinstaller" |
| `dhcp_range_start` | First IP in DHCP range | String | No | Calculated from network settings |
| `dhcp_range_end` | Last IP in DHCP range | String | No | Calculated from network settings |

## Dependencies

This role depends on the following roles, which it will call in sequence:
  - `pcofficina.netinstaller.debian_only`
  - `pcofficina.netinstaller.apt_update_cache`
  - `pcofficina.netinstaller.basepath`
  - `pcofficina.netinstaller.network`
  - `pcofficina.netinstaller.dhcp`
  - `pcofficina.netinstaller.router`
  - `pcofficina.netinstaller.memtest`
  - `pcofficina.netinstaller.iso_linuxmint`
  - `pcofficina.netinstaller.iso_win11`
  - `pcofficina.netinstaller.ipxe`
  - `pcofficina.netinstaller.tftp`
  - `pcofficina.netinstaller.nfs`
  - `pcofficina.netinstaller.samba`
  - `pcofficina.netinstaller.http`

## Example Playbook

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

## License

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.
