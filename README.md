ssh
===

Ansible role to create ssh client

* includes
* config entries to include includes

Requirements
------------

* [ansible.builtin](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/index.html)

Role Variables
--------------

* defaults

  * `main.yaml`

    ```yaml
    ssh_config: {}  # dict with ssh client config file attributes
      path: "~/.ssh/config"  # config file location
      owner: "{{ lookup('env','USER') }}"

    ssh_include: {}  # dict with ssh client include files attributes
      path: "{{ ssh_config['path'] | dirname }}/include"
      owner: "{{ lookup('env','USER') }}"
      options: {}  # options to add to each Host entry
        User: "{{ lookup('env','USER') }}"
        IdentityFile: ~/.ssh/id_rsa
        IdentitiesOnly: "yes"
        UserKnownHostsFile: ~/.ssh/known_hosts
    ```

Dependencies
------------

*No* *dependencies*

Tags
----

* **ssh.include** - Create ssh client includes
* **ssh.config** - Update ssh client config

Examples
--------

* `requirements.yaml`

  ```yaml
  - name: ssh
    src: https://github.com/mario-slowinski/ssh
  ```

* `playbook.yaml`

  ```yaml
  - hosts: servers
    gather_facts: false
    become: false
    connection: local  # create ssh includes locally

    roles:
      - role: ssh
  ```

License
-------

[GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.html)

Author Information
------------------

[mario.slowinski@gmail.com](mailto:mario.slowinski@gmail.com)
