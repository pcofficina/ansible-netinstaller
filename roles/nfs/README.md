<instructions>
Based on the provided context, generate the documentation as follows:

    Collection README (README.md):
        Provide a concise overview of the pcofficina.netinstaller collection's purpose (likely setting up a network boot/installation environment).
        Include standard installation instructions (e.g., ansible-galaxy collection install pcofficina.netinstaller).
        Crucially: Dedicate a prominent section to explaining the primary usage pattern outlined above. Detail the required variables and their purpose. Use the provided playbook as the canonical example.
        List the roles expected to be within the collection (including run and any others you infer) with a brief description of their likely contribution.
        Mention any presumed collection-level dependencies or requirements.

    Role READMEs (Individual README.md for each role):
        For the run role and all other roles you infer to be part of the collection:
            Create a separate README.md.
            Describe the specific purpose of the role and its presumed function within the collection's workflow.
            Detail the input parameters/variables the role likely accepts (name, description, type, default, required status), paying close attention to those used in the primary usage pattern.
            List any presumed dependencies (other roles, system packages, etc.).
            Provide relevant usage examples or snippets, particularly showing how the role fits into the overall primary usage pattern.

    Inference and Assumptions:
        Since the full collection source code is not available, you must infer the likely structure, functions, and parameters of the internal roles (beyond the run role).
        Base your inferences on:
            The collection's name (netinstaller).
            The primary usage pattern (variables, run role).
            Standard Ansible role design and naming conventions.
        Explicitly state any significant assumptions made about the collection's internal workings or role functionalities within the generated documentation (e.g., in a dedicated "Assumptions" section or inline).

    Quality Standards:
        The final documentation must be:
            Clear: Easy to follow for someone familiar with Ansible.
            Accurate: Faithfully represents the provided usage pattern.
            Detailed: Provides sufficient depth on configuration and operation.
            Comprehensive: Covers the collection overview and all inferred roles.
            Well-structured: Uses Markdown effectively for readability (headings, lists, code blocks).
            Actionable: Enables a user to confidently configure and use the collection for its primary purpose based only on reading the documentation. </instructions>

<output_format>
Present the generated documentation clearly demarcated into sections for the main Collection README and each inferred Role README. Specify the assumed names for the inferred roles. Use standard Markdown formatting throughout.
</output_format># Pcofficina.Netinstaller NFS Role

This role configures the NFS (Network File System) server for sharing Linux installation files over the network.

## Role Purpose

The `nfs` role:
1. Installs NFS server packages
2. Creates the necessary directory structure
3. Configures NFS exports for the installation directory
4. Sets appropriate permissions and ownership
5. Ensures the NFS server is running and enabled
6. Configures firewall rules if applicable

## Requirements

- No special requirements beyond the collection-level requirements

## Role Variables

### Required Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `netinstaller_nfs_dir` | NFS export directory | String | Yes | From common_vars |
| `network_lan_net` | Network address for the installation LAN | String | Yes | None |
| `network_lan_netmask` | Netmask for the installation network | String | Yes | None |

### Optional Variables

| Variable | Description | Type | Required | Default |
|----------|-------------|------|----------|---------|
| `nfs_server_package` | NFS server package to install | String | No | Determined by OS |
| `nfs_manage_firewall` | Whether to configure firewall rules | Boolean | No | true |
| `nfs_export_options` | NFS export options | String | No | "ro,sync,no_root_squash,no_subtree_check" |

## Dependencies

- `pcofficina.netinstaller.common_vars`

## Example Usage

```yaml
- name: Set up NFS server
  ansible.builtin.include_role:
    name: pcofficina.netinstaller.nfs
  vars:
    nfs_manage_firewall: true
    nfs_export_options: "ro,sync,no_root_squash,no_subtree_check,no_wdelay"
```

## License

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.
