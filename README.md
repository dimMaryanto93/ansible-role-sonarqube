`dimmaryanto93.docker`
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
- [community.docker](https://github.com/ansible-collections/community.docker)

Temen-temen bisa install, dengan cara 

```bash
ansible-galaxy collection install ansible.posix community.docker
```

Atau temen-temen bisa menggunakan `requirement.yaml` file and install menggunakan `ansible-galaxy collection install -r requirement.yaml`, dengan format seperti berikut:

```yaml
---
collections:
  - ansible.posix
  - community.docker
```

Role Variables
--------------

Ada beberapa variable yang temen-temen bisa gunakan untuk setting docker daemon, diantaranya seperti berikut:

| Variable name                           | Example value | Description |
| :---                                    | :---          | :---        |
| `docker_storage_driver`                 | `overlay2`    | Default value untuk driver storage adalah `overlay2` tapi temen-temen bisa ganti drivernya sesuai dengan dokumentasi [berikut](https://docs.docker.com/storage/storagedriver/select-storage-driver/) |
| `docker_insecure_registries_enabled`    | `false`       | Digunakan untuk meng-aktifkan insecure registry dalam `/etc/docker/daemon.json`, default value adalah `false` jika mau aktifkan confignya set jadi `true` |


Jika variable `docker_insecure_registries_enabled` bernilai `true`, kita perlu setup varible seperti berikut:

```yaml
docker_insecure_registries_conf:
  - url: "example.registry.com:8087"
    auth:
      docker_login: true      
      user: example
      password: secret
  - url: "other.registry.com"
    auth:
      docker_login: true      
      user: example2
      password: secret2
```

keterangan object tersebut:

| Variable name         | Example value                   | Description |
| :---                  | :---                            | :---        |
| `url`                 | `example.registry.com:8087`     | Adalah alamat dari insecure registry |
| `auth.docker_login`   | `true`                          | Digunakan untuk melakukan login ke insecure registry tersebut dengan menggunakan `username` dan `password` |
| `auth.user`           | `-`                             | Username yang digunakan untuk login ke insecure-registry |
| `auth.password`       | `-`                             | Password yang digunakan untuk login ke insecure-registry |

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
      - { role: dimmaryanto93.docker }
```

License
-------

MIT
