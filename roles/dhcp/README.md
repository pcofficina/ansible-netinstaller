# Pcofficina.Netinstaller DHCP Role

This role configures a DHCP server for the installation network, providing IP addresses and PXE boot information to client machines.

## Role Purpose

The `dhcp` role:
1. Installs and configures a Kea DHCP server
2. Sets up the DHCP subnet with appropriate address range
3. Configures PXE boot options needed for network installation
4. Ensures the DHCP service is running and enabled
5. Configures firewall rules if applicable

## Requirements

- No special requirements beyond the collection-level requirements

## Role Variables

### Required Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `network_lan_interface` | Interface for DHCP server | String | Yes | None |
| `network_lan_ip` | IP address of this server (used as next-server) | String | Yes | None |
| `network_lan_net` | Network address for the installation LAN | String | Yes | None |
| `network_lan_netmask` | Netmask for the installation network | String | Yes | None |

### Optional Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `dhcp_lan_ip_pool_start` | First IP in DHCP range | String | No | Automatically calculated |
| `dhcp_lan_ip_pool_end` | Last IP in DHCP range | String | No | Automatically calculated |

The DHCP pool range is automatically calculated to reserve approximately 80% of the IP addresses in the subnet. The reserved IPs are split between the beginning and end of the subnet range.

## Dependencies

- `pcofficina.netinstaller.common_vars`

## Example Usage

```yaml
- name: Set up DHCP server
  ansible.builtin.include_role:
    name: pcofficina.netinstaller.dhcp
  vars:
    network_lan_interface: "enp3s0"
    network_lan_ip: "192.168.192.1"
    network_lan_net: "192.168.192.0"
    network_lan_netmask: "24"
```

## License

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.
