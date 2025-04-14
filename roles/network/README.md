# Pcofficina.Netinstaller Network Role

This role configures the network interfaces required for the netinstaller environment, setting up the dedicated installation network for PXE booting and network-based OS installations.

## Role Purpose

The `network` role:
1. Configures the specified network interface with a static IP address
2. Ensures the interface is up and operational
3. Sets up network parameters required by other roles
4. Configures network settings persistently across reboots
5. Validates network configuration

## Requirements

- A dedicated network interface for the installation network
- Root/sudo access on the target system

## Role Variables

### Required Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `network_lan_interface` | Network interface to be used for installation LAN | String | Yes | None |
| `network_lan_ip` | IP address for the server on the installation network | String | Yes | None |
| `network_lan_net` | Network address for the installation LAN | String | Yes | None |
| `network_lan_netmask` | Netmask for the installation network in CIDR notation | String | Yes | None |

### Optional Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `network_lan_gateway` | Gateway for the installation network (if any) | String | No | None |
| `network_restart_method` | Method to use when restarting network (service, systemd, etc.) | String | No | Determined by OS |
| `network_manage_routes` | Whether to manage network routes | Boolean | No | false |

## Dependencies

- `pcofficina.netinstaller.common_vars`

## Example Usage

```yaml
- name: Configure network for netinstaller
  ansible.builtin.include_role:
    name: pcofficina.netinstaller.network
  vars:
    network_lan_interface: "enp3s0"
    network_lan_ip: "192.168.192.1"
    network_lan_net: "192.168.192.0"
    network_lan_netmask: "24"
```

## License

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.
