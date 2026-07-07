# ans-fleet

[![Ansible Lint](https://github.com/tonezzz/ans-fleet/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/tonezzz/ans-fleet/actions/workflows/ansible-lint.yml)

Ansible playbooks to set up Ubuntu desktops, Ubuntu servers, and Windows workstations.

## Supported profiles

| Profile | Playbook | Command |
|---------|----------|---------|
| Ubuntu desktop | `playbooks/ubuntu_desktop.yml` | `ansible-playbook playbooks/ubuntu_desktop.yml -K` |
| Ubuntu server | `playbooks/ubuntu_server.yml` | `ansible-playbook playbooks/ubuntu_server.yml -K` |
| Windows | `playbooks/windows_setup.yml` | `ansible-playbook playbooks/windows_setup.yml` |

## Quick start on a new Ubuntu PC

```bash
sudo apt update && sudo apt install -y ansible git
ansible-galaxy collection install community.general chocolatey.chocolatey

git clone https://github.com/tonezzz/ans-fleet.git
cd ans-fleet

# For local desktop setup
ansible-playbook playbooks/ubuntu_desktop.yml -K

# For a server
ansible-playbook playbooks/ubuntu_server.yml -K
```

## Configure hosts

Edit `inventory/hosts.yml` to match your machines. For local desktop setup, `localhost` is already configured.

## Secrets

Use Ansible Vault for sensitive data:

```bash
ansible-vault create group_vars/all/secrets.yml
```

Never commit the vault password file. Use `--ask-vault-pass` at runtime.

## Requirements

- `community.general` collection for Ubuntu package managers and UFW.
- `chocolatey.chocolatey` collection for Windows.

Install collections:

```bash
ansible-galaxy collection install -r requirements.yml
```

## Continuous integration

Every push and pull request to `main` is checked with `ansible-lint` via GitHub Actions.

## Notes

- Keep profile-specific variables in `group_vars/`.
- The desktop playbook includes `common`, `desktop`, and `dev_tools` roles.
- Add common tasks to the `common` role.
- Extend `desktop`, `server`, `windows`, or `dev_tools` roles for each profile.
