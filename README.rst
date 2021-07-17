Ansible role: pyenv
===================

|Tests|

.. |Tests| image:: https://github.com/staticdev/ansible-galaxy-pyenv/workflows/Tests/badge.svg
   :target: https://github.com/staticdev/ansible-galaxy-pyenv/actions?workflow=Tests
   :alt: Tests

Ansible Galaxy role for `pyenv`_ on Debian / Ubuntu / RedHat / OSX.

Install it with the following command:

.. code:: console

    $ ansible-galaxy install staticdev.pyenv

Requirements
------------

None.


Role Variables
--------------

Here is the list of all variables and their default values:

- `pyenv_env: "user"` (should be either `"user"` or `"system"`)
- `pyenv_path: "{% if pyenv_env == 'user' %}{{ ansible_env.HOME }}/pyenv{% else %}/usr/local/pyenv{% endif %}"`
- `pyenv_owner: "{{ ansible_env.USER }}"`
- `pyenv_python_versions: ["3.9.1"]`
- `pyenv_virtualenvs: [{ venv_name: "latest", py_version: "3.9.1" }]`
- `pyenv_global: ["3.9.1"]`
- `pyenv_update_git_install: no`
- `pyenv_enable_autocompletion: no`
- `pyenv_setting_path: "{% if pyenv_env == 'user' %}~/.bashrc{% else %}/etc/profile.d/pyenv.sh{% endif %}"`


Dependencies
------------

None.


Example Playbook
----------------

.. code:: yaml

    - hosts: servers
      roles:
         - role: staticdev.pyenv
           pyenv_path: "{{ home }}/pyenv"
           pyenv_owner: "{{ instance_owner }}"
           pyenv_global: 
             - "3.7.11"
           pyenv_update_git_install: no
           pyenv_enable_autocompletion: no
           pyenv_python_versions:
             - "3.8.11"
             - "3.9.6"
           pyenv_virtualenvs:
             - venv_name: "latest_v39"
               py_version: "3.9.6"
             - venv_name: "latest_v38"
               py_version: "3.8.11"


License
-------

MIT


Author Information
------------------

`staticdev`_. Heavily based on Maxim Avanov's `avanov.pyenv`_

.. _avanov.pyenv: https://galaxy.ansible.com/avanov/pyenv
.. _pyenv: https://github.com/yyuu/pyenv
.. _staticdev: https://github.com/staticdev
