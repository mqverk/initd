# initd

Production-ready Ansible project for Linux server bootstrap and static site hosting.

## What it configures

- Base system utilities
- Firewall and fail2ban baseline
- Nginx web server for static content
- Static app deployment from tarball or Git
- SSH key access and hardening

## Project layout

- `setup.yml`: main playbook
- `inventory/hosts.ini`: inventory example
- `group_vars/all.yml`: shared defaults
- `roles/base`: system and security baseline
- `roles/nginx`: web server installation and configuration
- `roles/app`: static app deployment logic
- `roles/ssh`: SSH key management and hardening

## Prerequisites

1. Install required collections:

   ```bash
   ansible-galaxy collection install -r collections/requirements.yml
   ```

2. Update inventory and variables to match your environment.

## Required variable inputs

Set at least one SSH public key before running production setup:

```yaml
ssh_public_keys:
  - "ssh-ed25519 AAAA... your-key"
```

## App source modes

### Tarball deployment

```yaml
app_source: tarball
app_tarball_url: https://example.com/static-site.tar.gz
app_tarball_strip_components: 1
```

### Git deployment

```yaml
app_source: git
app_git_repo: https://github.com/example/static-site.git
app_git_version: main
```

## Run commands

Full setup:

```bash
ansible-playbook setup.yml
```

App-only run:

```bash
ansible-playbook setup.yml --tags "app"
```
