# HPE MCP Packages Installation

This Ansible role installs HPE Management Component Pack (MCP) packages on Debian-based systems. It handles repository setup, GPG key management, and package installation for HPE server management tools.

## Requirements

- Debian-based operating system (tested on Debian/Ubuntu)
- Ansible 2.10 or higher
- Internet access to download HPE repository keys and packages
- Root or sudo access on target systems

## Role Variables

The following variables are available for customization:

### Repository Configuration
```yaml
# Base URL for the HPE MCP repository
hpe_mcp_pkgs_repo_url: "http://downloads.linux.hpe.com/SDR/repo/mcp"

# APT repository filename
hpe_mcp_pkgs_apt_filename: "hpe"

# Project version for the repository
hpe_mcp_pkgs_project_ver: "current"

# Base URL for HPE repository keys
hpe_mcp_pkgs_keys_base_url: "https://downloads.linux.hpe.com/SDR/"
```

### GPG Keys
```yaml
# List of GPG key files to download and import
hpe_mcp_pkgs_key_files:
  - hpPublicKey2048_key1.pub
  - hpePublicKey2048_key1.pub
  - hpePublicKey2048_key2.pub

# Path where the GPG keyring will be stored
hpe_mcp_pkgs_keyring_file: "/etc/apt/keyrings/hpe.gpg"
```

### Package Installation
```yaml
# List of HPE MCP packages to install
hpe_mcp_pkg_to_install:
  - amsd
  # - hponcfg
  # - ssacli
  # - ssaducli
  # - ssa
  # - lldpd
```

## Dependencies

This role has no dependencies on other Ansible roles.

## Example Playbook

```yaml
- hosts: hpe_servers
  roles:
    - role: hpe_mcp_packages
      vars:
        hpe_mcp_pkg_to_install:
          - amsd
          - ssacli
          - hponcfg
```

## Functionality

The role performs the following tasks:

1. Installs GPG for key management
2. Creates necessary directories for APT keyrings
3. Downloads and imports HPE repository GPG keys
4. Configures the HPE MCP repository
5. Installs specified HPE MCP packages

## License

BSD

## Author Information

This role was created in 2025 by [Simon Caron](https://simoncaron.com/).

## Notes

- The role currently supports Debian-based systems only
- Package installation errors are ignored in check mode
- Some packages are commented out by default in the package list - uncomment as needed