# Pcofficina.Netinstaller Samba Role

This role configures the Samba server for sharing Windows installation files over the network.

## Role Purpose

The `samba` role:
1. Installs Samba server packages
2. Creates the necessary directory structure
3. Configures Samba shares for Windows installation files
4. Sets appropriate permissions and ownership
5. Ensures the Samba server is running and enabled
6. Configures firewall rules if applicable

## Requirements

- No special requirements beyond the collection-level requirements

## Role Variables

### Required Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `netinstaller_samba_dir` | Samba share directory | String | Yes | From common_vars |
| `network_lan_net` | Network address for the installation LAN | String | Yes | None |
| `network_lan_netmask` | Netmask for the installation network | String | Yes | None |

### Optional Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `samba_server_package` | Samba server package to install | String | No | Determined by OS |
| `samba_manage_firewall` | Whether to configure firewall rules | Boolean | No | true |
| `samba_workgroup` | Windows workgroup name | String | No | "WORKGROUP" |
| `samba_share_name` | Name of the share for Windows installation files | String | No | "windows" |
| `samba_guest_access` | Whether to allow guest access | Boolean | No | true |

## Dependencies

- `pcofficina.netinstaller.common_vars`

## Example Usage

```yaml
- name: Set up Samba server
  ansible.builtin.include_role:
    name: pcofficina.netinstaller.samba
  vars:
    samba_workgroup: "NETINSTALL"
    samba_guest_access: false
    samba_share_name: "win_install"
```

## License

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.
