# Pcofficina.Netinstaller ISO_linuxmint Role

This role prepares Linux Mint installation files for network-based deployment by extracting the ISO and configuring the necessary files for network booting.

## Role Purpose

The `iso_linuxmint` role:
1. Downloads Linux Mint ISO (if not already present)
2. Extracts the ISO contents to the NFS export directory
3. Creates the necessary directory structure
4. Configures boot files for PXE/iPXE booting
5. Sets up the appropriate boot menu entries

## Requirements

- Sufficient disk space for Linux Mint ISO and extracted files
- Internet access (if downloading the ISO)

## Role Variables

### Required Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `netinstaller_nfs_dir` | Directory for NFS exports | String | Yes | From common_vars |

### Optional Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `linuxmint_iso_url` | URL to download Linux Mint ISO | String | No | Latest stable release URL |
| `linuxmint_iso_path` | Local path to ISO if already downloaded | String | No | "{{ netinstaller_data_dir }}/iso/linuxmint.iso" |
| `linuxmint_version` | Version of Linux Mint to install | String | No | "21.2" |
| `linuxmint_edition` | Linux Mint edition (Cinnamon, MATE, Xfce) | String | No | "Cinnamon" |

## Dependencies

- `pcofficina.netinstaller.common_vars`
- `pcofficina.netinstaller.nfs` (for sharing the installation files)

## Example Usage

```yaml
- name: Prepare Linux Mint installation files
  ansible.builtin.include_role:
    name: pcofficina.netinstaller.iso_linuxmint
  vars:
    linuxmint_version: "21.2"
    linuxmint_edition: "Cinnamon"
```

## License

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.
