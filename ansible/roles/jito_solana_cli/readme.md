# Jito-Solana CLI Role

This role installs and configures the Jito-Solana CLI, which is a fork of the Solana CLI with Jito Labs modifications for MEV (Maximal Extractable Value) operations.

## Overview

The Jito-Solana CLI role provides a standalone installation of the Jito-Solana command-line interface, following the same pattern as the `solana_cli` role. This role is designed to be used as a dependency for Jito validator roles and other roles that require Jito-Solana CLI functionality.

## Dependencies

- `rust_env`: Provides Rust environment setup
- `common`: Provides common system utilities and checks

## Variables

### Required Variables

- `jito_version`: The version of Jito-Solana to install (e.g., "2.2.16")
- `solana_user`: The user account for Solana installation
- `solana_user_dir`: The home directory for the Solana user
- `solana_installed_releases_dir`: Directory for storing Solana releases

### Optional Variables

- `build_from_source`: Whether to build from source (default: false)
- `use_official_repo`: Whether to use official Jito repository (default: false)
- `jito_official_repo`: URL for official Jito repository
- `jito_forked_repo`: URL for forked Jito repository

## Installation Methods

### Binary Installation (Default)

Downloads pre-built Jito-Solana binaries from the official S3 store and installs them.

### Source Installation

Clones the Jito-Solana repository and builds from source. Requires more time and system resources.

## Usage

### As a Standalone Role

```yaml
- hosts: jito_validators
  roles:
    - role: jito_solana_cli
      vars:
        jito_version: "2.2.16"
        build_from_source: false
```

### As a Dependency

```yaml
# In meta/main.yml
dependencies:
  - role: jito_solana_cli
    vars:
      jito_version: "{{ jito_version }}"
```

## Tasks

1. **Precheck**: Validates required variables and checks if installation is needed
2. **Install**: Installs Jito-Solana CLI (binary or source)
3. **Configure**: Performs post-installation configuration
4. **Verify**: Verifies the installation and CLI functionality

## Tags

- `jito_solana_cli`: Main role tag
- `jito_solana_cli.precheck`: Precheck tasks only
- `jito_solana_cli.install`: Installation tasks only
- `jito_solana_cli.config`: Configuration tasks only
- `jito_solana_cli.verify`: Verification tasks only

## Verification

The role verifies:

- Binary existence and permissions
- Correct version and client identifier (JitoLabs)
- Basic CLI functionality (help command)

## Notes

- This role is independent of the standard `solana_cli` role
- Designed specifically for Jito Labs validator operations
- Follows the same architectural patterns as `solana_cli` for consistency
