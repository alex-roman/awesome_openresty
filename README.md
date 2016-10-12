### Status
[![Build Status](https://travis-ci.org/prozacUa/ansible_role_test.svg?branch=master)](https://travis-ci.org/prozacUa/ansible_role_test)
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
- `ssl: 0` - Add SSL block to nginx.conf. Make sure you place default.key and default.crt into templates folder.
- `force_https: 0` - Redirect all the incoming traffic to HTTPS
- `CORS: 0` - Add headers for Cross Origin Resources Sharing
- `document_root: "/var/www/html"` - Customize root directory for default vhost
- `server_name: ansible_inventory_name` - Ansible hostname here by default
- `workers: auto` - Set number of simultaneously running processes. 
  Auto means nginx will get the number of cores on your box and run worker for each core. Limit this for dev/staging.
- `php7: 0` - Adds proxying of all .php reqyests to php-fpm. Plese, make sure php7.0 installed.
- `php5: 0` - The same as php7 but with different socket name. Both use unix-socket for interconnection instead of TCP-sockets.
- `stub_status: True` - Add link to server status page for conn tracking

#### ToDo
- LuaRocks support
- Nginx amplify integration
- uwsgi proxying
- php-fpm autodiscovery
- Add variables for multiple vhosts
- Generate Letsencrypt and/or self signed certificates
- ...wait for your comments and suggestions...
