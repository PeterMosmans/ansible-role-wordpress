Ansible Role: wordpress
=========

Build status for this role: [![Build Status](https://travis-ci.org/PeterMosmans/ansible-role-wordpress.svg)](https://travis-ci.org/PeterMosmans/ansible-role-wordpress)

This role installs, configures and/or updates WordPress.

Requirements
------------

MySQL, and Apache2.

Role Variables
--------------

Available variables are listed below, along with their default values. The defaults can be found in ```defaults/main.yml```.

**wordpress_sites**: A list with WordPress sites, their database (db_name), database username (db_user)  and  password (db_password), source directory (src) and installed plugins. Example:
```
  wordpress_sites:
    - name: mywebsite
      src: /var/www/mywebsite
      db_name: mydatabase
      db_user: mydatabaseuser
      db_password: mydatabasepassword
      plugins:
        - akismet
        - google-captcha
```

Note that you'll need to have the websites configured for the PeterMosmans.apache2 role. Example:
```
apache2_websites:
  - src: ../../myrole/files
    name: www.mysite.com.conf
```

**wordpress_remove**: A list of files which will be forcibly removed after installing WordPress. Default:
```
wordpress_remove:
  - readme.html
  - license.txt
  - wp-config-sample.php
  - wp-content/plugins/hello.php
  - wp-content/themes/twentyeleven
  - wp-content/themes/twentyfifteen
  - wp-content/themes/twentyfourteen
  - wp-content/themes/twentythirteen
  - wp-content/themes/twentytwelve
```

**www_group**: The group under which the webserver runs (reads content). Default:
```
www_group: www-data
```

Dependencies
------------

PeterMosmans.apache2


Example Playbook
----------------
```
- hosts: all
  become: yes
  become_method: sudo
  roles:
    - role: PeterMosmans.apache2
    - role: PeterMosmans.wordpress
  vars:
    - wordpress_sites:
      - name: mywebsite
        src: /var/www/mywebsite
        db_name: mydatabase
        db_user: mydatabaseuser
        db_password: mydatabasepassword
        plugins:
          - akismet
          - google-captcha
```


Use the `--tags update` to perform an update of the WordPress installation, as well as all plugins.

License
-------
GPLv3


Author Information
------------------
Created by Peter Mosmans. Feedback always welcome.
