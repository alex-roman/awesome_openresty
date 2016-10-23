[![Build Status](https://travis-ci.org/prozacUa/awesome_openresty.svg?branch=master)](https://travis-ci.org/prozacUa/awesome_openresty)

OpenResty is a bundle of Nginx web server with additional libraries and enhanced features set.
You can find more info on a [Github](https://github.com/openresty/lua-nginx-module) and official [Openresty.org](https://openresty.org)

#### What does this role do?
- Checks your current nginx and openresty installation, compares with latest version and update both if needed
- Configures **PHP 5/7 proxying** for you
- Configures **SSL** with strong cyphers and **DHParam**
- **Forcing** HTTP traffic rediretcion to **HTTPS** if configured
- Adds **CORS** headers if you set 'CORS: True' parameter
- **Validates** nginx.conf before reloading Nginx
- **Deletes .default** samples from nginx folder
- Has pre-configured **molecule**.yml for testing your adjustements

#### Parameters (here is default values)
- `openresty_ssl: 0` - Add SSL block to nginx.conf. Make sure you place default.key and default.crt into templates folder.
- `openresty_force_https: 0` - Redirect all the incoming traffic to HTTPS
- `openresty_CORS: 0` - Add headers for Cross Origin Resources Sharing
- `openresty_document_root: "/var/www/html"` - Customize root directory for default vhost
- `openresty_server_name: ansible_inventory_name` - Ansible hostname here by default
- `openresty_workers: auto` - Set number of simultaneously running processes.
  Auto means nginx will get the number of cores on your box and run worker for each core. Limit this for dev/staging.
- `openresty_php7: 0` - Adds proxying of all .php reqyests to php-fpm. Plese, make sure php7.0 installed.
- `openresty_php5: 0` - The same as php7 but with different socket name. Both use unix-socket for interconnection instead of TCP-sockets.
- `openresty_stub_status: True` - Add link to server status page for conn tracking. Available at '/stub_status'
- `openresty_ssl_crt'{{ inventory_hostname }}.crt'` - filename of your SSL certificate
- `openresty_ssl_key: '{{ inventory_hostname }}.key'` - filename of your SSL key.
- `openresty_http_string` - custom string you want to add in 'http' block. For example: 'log_format ...;'
- `openresty_server_string` - custom string you want to add in 'server' block. For example: 'charset utf-8;'
- `openresty_server_include` - filename in templates directory that will be copied to server and added into nginx.conf via 'include' statement. For example: 'rewrite_rules.conf'

#### Example
```
---
- hosts: all
  vars:
    openresty_ssl: False
    openresty_force_https: False
    openresty_CORS: True
    openresty_document_root: '/var/www/newsite'
    openresty_server_name: 'www.mysite.com'
    openresty_workers: 1
    openresty_php7: True
    openresty_php5: False
    openresty_stub_status: True
    openresty_ssl_crt: '{{ inventory_hostname }}'
    openresty_ssl_key: '{{ inventory_hostname }}'
    openresty_http_string: False
    openresty_server_string: False
    openresty_server_include: 'locations.conf'
  roles:
    - role: openresty
```

#### ToDo
- LuaRocks support
- Nginx amplify integration
- uwsgi proxying
- php-fpm autodiscovery
- Add variables for multiple vhosts
- Generate Letsencrypt and/or self signed certificates
- ...wait for your comments and suggestions...
