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

- `pyenv_version: "HEAD"` - check https://github.com/pyenv/pyenv/releases
- `pyenv_virtualenv_version: "HEAD"` - check https://github.com/pyenv/pyenv-virtualenv/releases
- `pyenv_update_version: "HEAD"` - usually do not have releases but one can specify a commit hash
- `pyenv_env: "user"` (should be either `"user"` or `"system"`)
- `pyenv_path: "{% if pyenv_env == 'user' %}{{ ansible_env.HOME }}/pyenv{% else %}/usr/local/pyenv{% endif %}"`
- `pyenvrc_path: "{{ pyenv_path }}"`
- `pyenv_owner: "{{ ansible_facts.user_id }}"`
- `pyenv_owner_group: "{{ pyenv_owner }}"`
- `pyenv_python_versions: [3.11.4]`
- `pyenv_virtualenvs: [{ venv_name: latest, py_version: 3.11.4 }]`
- `pyenv_global: [3.11.4]`
- `pyenv_update_git_install: true` (get latest pyenv from git)
- `pyenv_enable_autocompletion: false`
- `pyenv_enable_virtualenvs: true`
- `pyenv_shellrc_file: "{% if pyenv_env == 'user' %}~/.bashrc{% else %}/etc/profile.d/pyenv.sh{% endif %}"`
- `pyenv_tmpdir: (must be explicitly defined)` - env variable `TMPDIR` used by [python-build][python-build] as described in [Special Environment Variables][special-env-vars].
- `pyenv_python_build_build_path: (must be explicitly defined)` - env variable `PYTHON_BUILD_BUILD_PATH` used by [python-build][python-build] as described in [Special Environment Variables][special-env-vars].
- `pyenv_python_build_cache_path: (must be explicitly defined)` - env variable `PYTHON_BUILD_CACHE_PATH` used by [python-build][python-build] as described in [Special Environment Variables][special-env-vars].
- `pyenv_python_build_mirror_url: (must be explicitly defined)` - env variable `PYTHON_BUILD_MIRROR_URL` used by [python-build][python-build] as described in [Special Environment Variables][special-env-vars].
- `pyenv_python_build_mirror_url_skip_checksum: (must be explicitly defined)` - env variable `PYTHON_BUILD_MIRROR_URL_SKIP_CHECKSUM` used by [python-build][python-build] as described in [Special Environment Variables][special-env-vars].
- `pyenv_python_build_skip_mirror: (must be explicitly defined)` - env variable `PYTHON_BUILD_SKIP_MIRROR` used by [python-build][python-build] as described in [Special Environment Variables][special-env-vars].
- `pyenv_python_build_skip_homebrew: (must be explicitly defined)` - env variable `PYTHON_BUILD_SKIP_HOMEBREW` used by [python-build][python-build] as described in [Special Environment Variables][special-env-vars].
- `pyenv_python_build_root: (must be explicitly defined)` - env variable `PYTHON_BUILD_ROOT` used by [python-build][python-build] as described in [Special Environment Variables][special-env-vars].
- `pyenv_python_build_definitions: (must be explicitly defined)` - env variable `PYTHON_BUILD_DEFINITIONS` used by [python-build][python-build] as described in [Special Environment Variables][special-env-vars].
- `pyenv_python_configure_opts: (must be explicitly defined)` - env variable `PYTHON_CONFIGURE_OPTS` used by [python-build][python-build] as described in [Special Environment Variables][special-env-vars].
- `pyenv_python_cflags: (must be explicitly defined)` - env variable `PYTHON_CFLAGS` used by [python-build][python-build] as described in [Special Environment Variables][special-env-vars].
- `pyenv_python_make_opts: (must be explicitly defined)` - env variable `PYTHON_MAKE_OPTS` used by [python-build][python-build] as described in [Special Environment Variables][special-env-vars].
- `pyenv_python_make_install_opts: (must be explicitly defined)` - env variable `PYTHON_MAKE_INSTALL_OPTS` used by [python-build][python-build] as described in [Special Environment Variables][special-env-vars].
- `pyenv_configure_opts: (must be explicitly defined)` - env variable `CONFIGURE_OPTS` used by [python-build][python-build] as described in [Special Environment Variables][special-env-vars].
- `pyenv_cc: (must be explicitly defined)` - env variable `CC` used by [python-build][python-build] as described in [Special Environment Variables][special-env-vars].
- `pyenv_make: (must be explicitly defined)` - env variable `MAKE` used by [python-build][python-build] as described in [Special Environment Variables][special-env-vars].
- `pyenv_make_opts: (must be explicitly defined)` - env variable `MAKE_OPTS` used by [python-build][python-build] as described in [Special Environment Variables][special-env-vars].
- `pyenv_make_install_opts: (must be explicitly defined)` - env variable `MAKE_INSTALL_OPTS` used by [python-build][python-build] as described in [Special Environment Variables][special-env-vars].
- `pyenv_profile_task: (must be explicitly defined)` - env variable `PROFILE_TASK` to customize the task used for profile guided optimization as described in [building Python for maximum performance][max-performance]. See also [here](https://docs.python.org/3/using/configure.html#cmdoption-enable-optimizations).
- `pyenv_custom_pyenvrc_file: (must be explicitly defined)` - path to a custom `.pyenvrc` shell file that will be sourced from `{{ pyenvrc_path }}/.pyenvrc`. It allows you to freely customize the environment to be used during `pyenv` execution. If defined, this file will be copied as `{{ pyenvrc_path }}/.pyenvrc.custom`.
- `pyenv_install_extra_opts: ("" -no extra options added-)` - check output of `pyenv install --help` for available additional options.

## Dependencies

None.

## Example Playbook

```yaml
- hosts: servers
  roles:
    - role: staticdev.pyenv
      vars:
        pyenv_version: "v2.3.9"
        pyenv_virtualenv_version: "v1.1.5"
        pyenv_update_version: "810db78"
        pyenv_shellrc_file: "{{ ansible_env.HOME }}/.shrc"
        pyenv_path: "{{ ansible_env.HOME }}/.pyenv"
        pyenvrc_path: "{{ ansible_env.HOME }}"
        pyenv_owner: "{{ instance_owner }}"
        pyenv_global:
          - 3.11.4
          - 3.10.12
        pyenv_enable_autocompletion: false
        pyenv_python_versions:
          - 3.11.4
          - 3.10.12
        pyenv_virtualenvs:
          - venv_name: latest_v311
            py_version: 3.11.4
          - venv_name: latest_v310
            py_version: 3.10.12
        pyenv_make_opts: "-j4"
        pyenv_python_configure_opts: "--enable-optimizations --with-lto --with-ensurepip=upgrade"
        pyenv_python_cflags: "-march=native -mtune=native"
        pyenv_profile_task: "-m test.regrtest --pgo -j0"
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
[python-build]: https://github.com/pyenv/pyenv/tree/master/plugins/python-build "python-build plugin"
[special-env-vars]: https://github.com/pyenv/pyenv/blob/master/plugins/python-build/README.md#special-environment-variables "Special environment variables"
[max-performance]: https://github.com/pyenv/pyenv/blob/master/plugins/python-build/README.md#building-for-maximum-performance "Building for maximum performance"
