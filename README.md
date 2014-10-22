modcloth.nginx-nr-agent
=========

This role installs and configures nginx-nr-agent (http://nginx.com/nr-plugin/).

Requirements
------------

None.

Role Variables
--------------

```yml
new_relic_license_key: # New Relic license key

nginx_nr_agent_apt_repository: # apt repository containing nginx-nr-agent (see http://nginx.org/en/linux_packages.html)
nginx_nr_agent_config_template: # template to use to generate ini config using template module (if empty, none is written)

# Below is a list of variables that can be used with the default template:

nginx_nr_agent_poll_interval: # interval to poll nginx sources

# list of loggers (dicts)
nginx_nr_agent_loggers:
# dictionary fields include:
# name (required): name of the logger
# handlers (required): list of handler names (defined below)
# level (optional): level of the logger

# list of handlers (dicts)
nginx_nr_agent_handlers:
# dictionary fields include:
# name (required): name of the handler
# class (required): class name of logger
# formatter (required): name of formatter to use (defined below)
# level (optional): level of the logger
# args (optional): args to pass to class initializer

# list of formatters (dicts)
nginx_nr_agent_formatters:
# dictionary fields include:
# name (required): name of the handler
# format (required): format of messages
# datefmt (optional): format of timestamps in messages

# list of formatters (sources)
nginx_nr_agent_sources: []
# dictionary fields include:
# name (required): name of the source
# url (required): URL to poll for nginx status
# http_user (optional): user to use for HTTP basic auth
# http_password (optional): password to use for HTTP basic auth
```

Defaults are provided which match the default ini file (see
`defaults/main.yml`) shipped with nginx-nr-agent.

Dependencies
------------

None.

Example Playbook
----------------

```yml
- hosts: servers
  sudo: true
  roles:
  - role: modcloth.nginx-nr-agent
    new_relic_license_key: 'ABCD'
    nginx_nr_agent_poll_interval: 10
    nginx_nr_agent_sources:
      name: 'FOO'
      url: 'http://example.com:80/stats'
```

License
-------

MIT

Author Information
------------------

ModCloth, Inc.
