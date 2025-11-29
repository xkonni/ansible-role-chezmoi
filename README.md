# Ansible Chezmoi

Installs [chezmoi](https://www.chezmoi.io/) on Linux servers.

## Role Variables

Available variables are listed below, along with default values (see [`defaults/main.yml`](defaults/main.yml)):

The role downloads and installs chezmoi using the official install script from `https://get.chezmoi.io`. The binary is installed to `~/bin/chezmoi`.

```yaml
chezmoi_init_url: ""
```

Set this to the URL of a repository with chezmoi's dotfiles you want to use. This option is passed as-is to chezmoi, which means you can use all kinds of options that chezmoi supports. For example, if your repo is on Github with the name `dotfiles`, then you can just set this variable to your Github username.

If you don't set this variable, then `chezmoi init` will be run without any options.

```yaml
chezmoi_cleanup: false
```

Set this to `true` to enable cleanup tasks before running `chezmoi init`. This will check for incomplete oh-my-zsh installations and remove them to prevent conflicts with chezmoi's dotfile management. Useful when re-running the role on a system that may have partial installations.

**Example override for a single run:**
```bash
ansible-playbook chezmoi.yml -e "chezmoi_cleanup=true"
```

```yaml
chemzoi_apply: true
```

Set this to `false` to skip applying chezmoi configuration. When `true`, the role will run `chezmoi apply` to deploy dotfiles.

```yaml
chemzoi_apply_ignore_errors: false
```

Set this to `true` to continue execution even if `chezmoi apply` fails. Useful when some dotfile operations may fail but you want the playbook to continue.

## Dependencies

None.

## Example Playbook

```yaml
- hosts: servers
  roles:
    - role: ansible-role-chezmoi
      chezmoi_init_url: "github_username"
```

With cleanup and forced apply:

```yaml
- hosts: servers
  roles:
    - role: ansible-role-chezmoi
      chezmoi_init_url: "https://github.com/username/dotfiles.git"
      chezmoi_cleanup: true
      chezmoi_apply: true
```

## License

[MIT](LICENSE)
