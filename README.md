# ans-fleet

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

git clone https://github.com/YOUR_USERNAME/ans-fleet.git
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

## Notes

- Keep profile-specific variables in `group_vars/`.
- Add common tasks to the `common` role.
- Extend `desktop`, `server`, or `windows` roles for each profile.
