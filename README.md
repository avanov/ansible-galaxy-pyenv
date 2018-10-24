avanov.pyenv
============

[![Build Status](https://travis-ci.org/avanov/ansible-galaxy-pyenv.svg)](https://travis-ci.org/avanov/ansible-galaxy-pyenv)


Ansible Galaxy role for [pyenv](https://github.com/yyuu/pyenv) on Ubuntu / RedHat / OSX.

Install it with the following command:

```bash
$ ansible-galaxy install avanov.pyenv
```

Requirements
------------

None

Role Variables
--------------

Here is the list of all variables and their default values:

* ``pyenv_env: "user"``
* ``pyenv_path: "{% if pyenv_env == 'user' %}{{ ansible_env.HOME }}/pyenv{% else %}/usr/local/pyenv{% endif %}"``
* ``pyenv_owner: "{{ ansible_env.USER }}"``
* ``pyenv_python_versions: ["3.4.1"]``
* ``pyenv_virtualenvs: [{ venv_name: "latest", py_version: "3.4.1" }]``
* ``pyenv_global: "3.4.1"``
* ``pyenv_update_git_install: no``
* ``pyenv_enable_autocompletion: no``
* ``pyenv_setting_path: "{% if pyenv_env == 'user' %}~/.bashrc{% else %}/etc/profile.d/pyenv.sh{% endif %}"``

Dependencies
------------

None

Example Playbook
-------------------------

    - hosts: servers
      roles:
         - role: avanov.pyenv
           pyenv_path: "{{ home }}/pyenv"
           pyenv_owner: "{{ instance_owner }}"
           pyenv_global: "3.6.5"
           pyenv_update_git_install: no
           pyenv_enable_autocompletion: no
           pyenv_python_versions:
             - "3.6.5"
             - "3.4.1"
             - "2.7.8"
           pyenv_virtualenvs:
             - venv_name: "latest_v3"
               py_version: "3.4.1"

             - venv_name: "latest_v2"
               py_version: "2.7.8"

License
-------

MIT

Author Information
------------------

Maxim Avanov (https://maximavanov.com/)
