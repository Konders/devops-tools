- [Install multiple apt packages](#install-multiple-apt-packages)
- [Remove file](#remove-file)
- [Create SymLinks](#create-symlink)

## Install multiple apt packages
You need to pass packages' names into `pkg` of module `apt`
```yaml
- name: Install apt packages
  become: true
  apt:
    update_cache: true
    cache_valid_time: 3600 # Update the apt cache only if it’s older than 3,600 seconds (1 hour).
    pkg:
      - acl
      - git
      - libjpeg-dev
      - libpq-dev
      - memcached
      - nginx
      - postgresql
      - python3-dev
      - python3-pip
      - python3-venv
      - python3-psycopg2
      - supervisor
```

## Remove file

To remove a file:
```yaml
- name: Remove default nginx conf
  become: true
  file:
    path: /etc/nginx/sites-enabled/default
    state: absent
```

## Create SymLink

To create sylinks, in cases such as enabling a nginx site (sites-available -> sites-enabled), we can use module `file` as below:
```yaml
- name: Enable the nginx config filebecome: true
  file:
    src: /etc/nginx/sites-available/mezzanine.conf
    dest: /etc/nginx/sites-enabled/mezzanine.conf
    state: link
    mode: 0777
```
As shown in above example, we use the file module to create the symlink and to remove the default config file. This module is useful for creating directories, symlinks, and empty files; deleting files, directories, and symlinks; and setting properties such as permissions and ownership.
[ref: page-177 of ebook `Ansible Up and Running, 3rd Edition Sixth Early Release`]