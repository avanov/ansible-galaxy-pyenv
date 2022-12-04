# Ansible role: Pyenv

[![Tests](https://github.com/staticdev/ansible-galaxy-pyenv/workflows/Tests/badge.svg)][tests]

[tests]: https://github.com/staticdev/ansible-galaxy-pyenv/actions?workflow=Tests

Ansible Galaxy role for [pyenv] on Debian / Ubuntu / RedHat / OSX.

Install it with the following command:

```console
$ ansible-galaxy install staticdev.pyenv
```

## Requirements

None.

## Role Variables

Here is the list of all variables and their default values:

- `pyenv_env: "user"` (should be either `"user"` or `"system"`)
- `pyenv_path: "{% if pyenv_env == 'user' %}{{ ansible_env.HOME }}/pyenv{% else %}/usr/local/pyenv{% endif %}"`
- `pyenv_owner: "{{ ansible_env.USER }}"`
- `pyenv_owner_group: "{{ pyenv_owner }}"`
- `pyenv_python_versions: [3.11.0]`
- `pyenv_virtualenvs: [{ venv_name: latest, py_version: 3.11.0 }]`
- `pyenv_global: [3.11.0]`
- `pyenv_update_git_install: true` (get latest pyenv from git)
- `pyenv_enable_autocompletion: false`
- `pyenv_enable_virtualenvs: true`
- `pyenv_setting_path: "{% if pyenv_env == 'user' %}~/.bashrc{% else %}/etc/profile.d/pyenv.sh{% endif %}"`

## Dependencies

None.

## Example Playbook

```yaml
- hosts: servers
  roles:
    - role: staticdev.pyenv
      pyenv_path: "{{ home }}/pyenv"
      pyenv_owner: "{{ instance_owner }}"
      pyenv_global:
        - 3.11.0
        - 3.10.6
      pyenv_enable_autocompletion: false
      pyenv_python_versions:
        - 3.11.0
        - 3.10.6
      pyenv_virtualenvs:
        - venv_name: latest_v311
          py_version: 3.11.0
        - venv_name: latest_v310
          py_version: 3.10.6
```

## License

Distributed under the terms of the [MIT] license,
_Ansible role Pyenv_ is free and open source software.

## Author Information

[staticdev]. Heavily based on Maxim Avanov's [avanov.pyenv]

[avanov.pyenv]: https://galaxy.ansible.com/avanov/pyenv
[mit]: https://opensource.org/licenses/MIT
[pyenv]: https://github.com/yyuu/pyenv
[staticdev]: https://github.com/staticdev
