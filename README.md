Role Name
========

Ansible Galaxy role for [pyenv](https://github.com/yyuu/pyenv) on Ubuntu.

Requirements
------------

None

Role Variables
--------------

Here is the list of all variables and their default values:

* ``pyenv_path: "{{ ansible_env.HOME }}/pyenv"``
* ``pyenv_owner: "{{ ansible_env.USER }}"``
* ``pyenv_python_versions: ["3.4.0"]``


Dependencies
------------

None

Example Playbook
-------------------------

    - hosts: servers
      roles:
         - {role: avanov.pyenv,
            pyenv_path: "{{ home }}/pyenv",
            pyenv_owner: "{{ instance_owner }}",
            pyenv_python_versions: ["3.4.0", "2.7.6"]}

License
-------

MIT

Author Information
------------------

Maxim Avanov (https://maximavanov.com/)
