# Pcofficina.Netinstaller Router Role

This role configures the netinstaller server to act as a router, allowing clients on the installation network to access external networks (like the internet) for package downloads during installation.

## Role Purpose

The `router` role:
1. Enables IP forwarding on the system
2. Configures NAT using iptables or nftables
3. Sets up proper routing between network interfaces
4. Ensures persistence of routing configuration
5. Configures firewall rules as needed

## Requirements

- At least two network interfaces (one for installation LAN, one for external connectivity)
- Root/sudo access on the target system

## Role Variables

### Required Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `network_lan_interface` | Network interface for the installation LAN | String | Yes | None |
| `network_wan_interface` | Network interface for external connectivity | String | Yes | None |

### Optional Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `router_enable_nat` | Whether to enable NAT for outgoing connections | Boolean | No | true |
| `router_forward_ports` | List of ports to forward from WAN to LAN | List | No | [] |
| `router_firewall_type` | Firewall type to use (iptables, nftables, firewalld) | String | No | Determined by OS |
| `router_persistent_config` | Whether to make routing config persistent | Boolean | No | true |

## Dependencies

- `pcofficina.netinstaller.common_vars`
- `pcofficina.netinstaller.network` (for network interface configuration)

## Example Usage

```yaml
- name: Configure routing
  ansible.builtin.include_role:
    name: pcofficina.netinstaller.router
  vars:
    network_wan_interface: "enp1s0"
    router_enable_nat: true
    router_forward_ports:
      - { proto: tcp, port: 22 }
```

## License

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.
