Nginx with http2 support
=========

This role compiles Nginx from source with HTTP/2 support, pagespeed and lua support.

Credits
-------

The steps for compiling openssl and nginx with http/2 support were taken from AJMaxwell's bash script (https://gist.github.com/AJMaxwell/f6793605068813aae888216b02364d85). There are only a few modifications to the dependencies. Credit also goes to mrbdmm who came up with the initial steps in a DigitalOcean thread: https://www.digitalocean.com/community/questions/how-to-get-already-installed-nginx-to-use-openssl-1-0-2-for-alpn

Supported Distributons
----------------------

This was only tested in Ubuntu 16.04 (xenial) and Debian 8 (jessie).

Requirements
------------

You will need to configure SSL and update the nginx virtual host file.

Role Variables
--------------

There is one manadatory variable you have to set:
      
      destination: /home/user

We need to run some of the compilation commands (such as make test) as unpriviledged user. The best way to do that is to download everything in a user's home folder rather than a more typical destination like /opt

And some optional variables with the versions you want to install. If not specified it will default to the following:

      nginx_version: 1.11.2
      openssl_version: 1.0.2j
      nps_version: 1.11.33.2
      luajit_version: 2.0.4
      luajit_major_version: 2.0
      lua_nginx_module_version: 0.10.7 
      ngx_devel_kit_version: 0.3.0

Example Playbook
----------------

This is how you would use this in your playbook:

    - hosts: servers
      vars:
        include_lua: false # to compile without lua
        destination: /home/user
      roles:
         - { role: tzumby.nginx-http2 }

License
-------

BSD
