# Pcofficina.Netinstaller Memtest Role

This role integrates Memtest86+ into the PXE boot environment, allowing network clients to boot directly into memory testing.

## Role Purpose

The `memtest` role:
1. Downloads the Memtest86+ binary
2. Prepares it for network booting

## Requirements

- TFTP server (configured by the tftp role)
- iPXE boot environment (configured by the ipxe role)

## Role Variables

### Required Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `memtest_dir` | Name of the memtest directory | String | No | memtest  |
| `memtest_basedir` | Full path of the memtest | String | No | "{{ basepath_dir }}/{{ memtest_dir }}" |

: memtest
memtest_basedir

### Optional Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `memtest_version` | Version of Memtest86+ to use | String | No | "7.20" |
| `memtest_baseurl` | Base URL to download Memtest86+ | String | No |  "https://www.memtest.org/download/v{{ memtest_version }}/" |
| `memtest_archive_name` | Name of Memtest86+ archive | String | No | "mt86plus_{{ memtest_version }}.binaries.zip" |
| `memtest_archive_url` | Full URL to download Memtest86+ archive | String | No | "{{ memtest_baseurl }}/{{ memtest_archive_name }}" |
| `memtest_archive_sha256` | Full URL to download sha256 hash of the Memtest86+ archive | String | No | "{{ memtest_baseurl }}/sha256sum.txt" |
| `memtest_exes` | Specific binaries to extract from Memtest86+ archive | String | No | memtest64.bin, memtest64.efi |

## Dependencies

- `pcofficina.netinstaller.common_vars`

## Example Usage

```yaml
- name: Set up Memtest86+
  ansible.builtin.include_role:
    name: pcofficina.netinstaller.memtest
  vars:
    memtest_version: "7.10"
```

## License

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.
