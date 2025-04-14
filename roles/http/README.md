# Pcofficina.Netinstaller HTTP Role

This role configures an HTTP server to host boot files, scripts, and resources needed for network-based installations.

## Role Purpose

The `http` role:
1. Installs an HTTP server (Nginx)
2. Creates the necessary directory structure
3. Configures the server to serve files from the designated directory
4. Sets appropriate permissions and ownership
5. Ensures the HTTP server is running and enabled

## Requirements

- No special requirements beyond the collection-level requirements

## Role Variables

### Required Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `netinstaller_http_dir` | HTTP server root directory | String | Yes | From common_vars |
| `network_lan_interface` | Network interface for HTTP service | String | Yes | None |

### Optional Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `http_server` | HTTP server to use (apache or nginx) | String | No | "apache" |
| `http_server_package` | HTTP server package to install | String | No | Determined by OS and http_server |
| `http_manage_firewall` | Whether to configure firewall rules | Boolean | No | true |
| `http_server_port` | Port for the HTTP server | Integer | No | 80 |

## Dependencies

- `pcofficina.netinstaller.common_vars`

## Example Usage

```yaml
- name: Set up HTTP server
  ansible.builtin.include_role:
    name: pcofficina.netinstaller.http
  vars:
    http_server: "nginx"
    http_server_port: 8080
```

## License

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.
