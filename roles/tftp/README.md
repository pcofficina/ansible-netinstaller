# Pcofficina.Netinstaller TFTP Role

This role sets up a TFTP (Trivial File Transfer Protocol) server needed for PXE boot operations.

## Role Purpose

The `tftp` role:
1. Installs and configures a TFTP server
2. Creates the necessary directory structure
3. Sets appropriate permissions
4. Ensures the service is running and enabled
5. Configures firewall rules if applicable

## Requirements

- No special requirements beyond the collection-level requirements

## Role Variables

### Required Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `netinstaller_tftp_dir` | TFTP root directory | String | Yes | From common_vars |
| `network_lan_interface` | Network interface for TFTP service | String | Yes | None |

### Optional Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `tftp_server_package` | TFTP server package to install | String | No | Determined by OS |
| `tftp_manage_firewall` | Whether to configure firewall rules | Boolean | No | true |
| `tftp_server_options` | Additional TFTP server options | Dictionary | No | {} |

## Dependencies

- `pcofficina.netinstaller.common_vars`

## Example Usage

```yaml
- name: Set up TFTP server
  ansible.builtin.include_role:
    name: pcofficina.netinstaller.tftp
  vars:
    tftp_manage_firewall: true
    tftp_server_options:
      timeout: 5
      retries: 3
```

## License

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.
