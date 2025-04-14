# Pcofficina.Netinstaller iPXE Role

This role sets up the iPXE boot environment which provides advanced network boot capabilities beyond standard PXE, including HTTP boot, menu systems, and scripting.

## Role Purpose

The `ipxe` role:
1. Installs iPXE packages or builds from source if necessary
2. Creates iPXE boot menu configuration files
3. Sets up iPXE chain loading from standard PXE
4. Configures boot menu entries for available operating systems
5. Places all necessary files in the TFTP and HTTP directories

## Requirements

- TFTP server (configured by the tftp role)
- HTTP server (configured by the http role)

## Role Variables

### Required Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `netinstaller_tftp_dir` | TFTP root directory | String | Yes | From common_vars |
| `netinstaller_http_dir` | HTTP server root directory | String | Yes | From common_vars |
| `network_lan_ip` | IP address for the server on the installation network | String | Yes | None |

### Optional Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `ipxe_build_from_source` | Whether to build iPXE from source | Boolean | No | false |
| `ipxe_source_repo` | Git repository for iPXE source | String | No | "https://github.com/ipxe/ipxe.git" |
| `ipxe_menu_timeout` | Timeout for boot menu in seconds | Integer | No | 30 |
| `ipxe_default_boot` | Default boot option if timeout expires | String | No | "local" |

## Dependencies

- `pcofficina.netinstaller.common_vars`
- `pcofficina.netinstaller.tftp` (for serving boot files)
- `pcofficina.netinstaller.http` (for serving iPXE scripts and files)

## Example Usage

```yaml
- name: Configure iPXE boot environment
  ansible.builtin.include_role:
    name: pcofficina.netinstaller.ipxe
  vars:
    ipxe_menu_timeout: 60
    ipxe_default_boot: "linux_mint"
```

## License

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.
