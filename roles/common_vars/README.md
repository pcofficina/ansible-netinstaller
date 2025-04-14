# Pcofficina.Netinstaller Common_vars Role

This role defines common variables and validates requirements across all roles in the PCOfficina Netinstaller collection.

## Role Purpose

The `common_vars` role:
1. Defines default values for shared variables
2. Validates that required variables are set correctly
3. Calculates derived values used by other roles
4. Ensures consistent configuration across the collection

## Requirements

None beyond the collection-level requirements.

## Role Variables

### Required Variables (defined at collection level)

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `network_lan_interface` | Network interface to be used for installation LAN | String | Yes | None |
| `network_lan_ip` | IP address for the server on the installation network | String | Yes | None |
| `network_lan_net` | Network address for the installation LAN | String | Yes | None |
| `network_lan_netmask` | Netmask for the installation network in CIDR notation | String | Yes | None |
| `dhcp_lan_interface` | Interface for DHCP server | String | Yes | None |

### Variables Defined by This Role

| Variable | Description | Type | Calculated From |
|----------|-------------|------|----------------|
| `netinstaller_data_dir` | Directory to store installation files | String | Default: "/opt/netinstaller" |
| `netinstaller_tftp_dir` | TFTP root directory | String | Default: "{{ netinstaller_data_dir }}/tftp" |
| `netinstaller_http_dir` | HTTP server root directory | String | Default: "{{ netinstaller_data_dir }}/http" |
| `netinstaller_nfs_dir` | NFS export directory | String | Default: "{{ netinstaller_data_dir }}/nfs" |
| `netinstaller_samba_dir` | Samba share directory | String | Default: "{{ netinstaller_data_dir }}/samba" |
| `dhcp_range_start` | First IP in DHCP range | String | Based on network_lan_net and netmask |
| `dhcp_range_end` | Last IP in DHCP range | String | Based on network_lan_net and netmask |

## Dependencies

None.

## Example Usage

This role is not typically used directly but is instead called by the `run` role. However, if needed, it can be included separately:

```yaml
- name: Include common variables
  ansible.builtin.include_role:
    name: pcofficina.netinstaller.common_vars
```

## License

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.
