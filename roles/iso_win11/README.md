# Pcofficina.Netinstaller ISO_win11 Role

This role prepares Windows 11 installation files for network-based deployment by extracting the ISO and configuring the necessary files for network booting via Samba.

## Role Purpose

The `iso_win11` role:
1. Processes a Windows 11 ISO (user-provided, as it cannot be automatically downloaded)
2. Extracts the ISO contents to the Samba share directory
3. Creates the necessary directory structure
4. Configures boot files for PXE/iPXE booting
5. Creates the appropriate boot menu entries
6. Sets up Windows PE environment if configured

## Requirements

- Windows 11 ISO file (must be provided by the user)
- Sufficient disk space for Windows 11 ISO and extracted files

## Role Variables

### Required Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `netinstaller_samba_dir` | Directory for Samba shares | String | Yes | From common_vars |
| `win11_iso_path` | Path to Windows 11 ISO file | String | Yes | None |

### Optional Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `win11_editions` | List of Windows 11 editions to make available | List | No | ["Professional", "Home"] |
| `win_pe_support` | Whether to set up Windows PE environment | Boolean | No | true |
| `win_auto_install` | Whether to enable unattended installation | Boolean | No | false |
| `win_auto_install_template` | Path to autounattend.xml template | String | No | None |

## Dependencies

- `pcofficina.netinstaller.common_vars`
- `pcofficina.netinstaller.samba` (for sharing the installation files)

## Example Usage

```yaml
- name: Prepare Windows 11 installation files
  ansible.builtin.include_role:
    name: pcofficina.netinstaller.iso_win11
  vars:
    win11_iso_path: "/path/to/windows11.iso"
    win11_editions: ["Professional", "Education"]
    win_auto_install: true
```

## License

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.
