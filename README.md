`dimmaryanto93.sonarqube`
=========

Repository ini digunakan untuk menginstall [Docker](https://docs.docker.com/engine/install/) untuk Linux

Support platform

- Debian
- Ubuntu
- CentOS


Ansible - User Guide
------------

Persiapan yang harus di lalukan, diantaranya

1. Create new user on your server, Recomend using **very-very Strong Password** or using password generator. 
  ```bash
  adduser <username>
  ```

2. Granted to sudoers with NOPASSWD, using `visudo`
  ```ini
  username    ALL=(ALL) NOPASSWD:ALL
  ```

3. Authenticate with private-key for login ssh, generate ssh key on your local machine then use `ssh-copy-id user@your-ip-server` to copy public key to your server.


Requirements
------------

Untuk menggunakan role ini, kita membutuhkan package/collection 

- [ansible.posix](https://github.com/ansible-collections/ansible.posix)

Temen-temen bisa install, dengan cara 

```bash
ansible-galaxy collection install ansible.posix
```

Atau temen-temen bisa menggunakan `requirement.yaml` file and install menggunakan `ansible-galaxy collection install -r requirement.yaml`, dengan format seperti berikut:

```yaml
---
collections:
  - ansible.posix
```

Role Variables
--------------

Ada beberapa variable yang temen-temen bisa gunakan untuk setting docker daemon, diantaranya seperti berikut:

| Variable name                           | Example value                                 | Description |
| :---                                    | :---                                          | :---        |
| `java_bin_path`                         | `/usr/lib/jvm/jdk-17-oracle-x64/bin/java`     | Default value untuk java binnary path |


Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: servers
  become: true
  roles:
      - { role: dimmaryanto93.sonarqube }
```

License
-------

MIT
