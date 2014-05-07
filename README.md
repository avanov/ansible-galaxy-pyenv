Role Name
========

Ansible Galaxy role for [pyenv](https://github.com/yyuu/pyenv) on Ubuntu.

Requirements
------------

None

Role Variables
--------------

* ``pyenv_owner``
* ``pyenv_path``
* ``pyenv_python_versions``


Dependencies
------------

None

Example Playbook
-------------------------

    - hosts: servers
      roles:
         - { role: pyenv }

License
-------

MIT

Author Information
------------------

Maxim Avanov (https://maximavanov.com/)
