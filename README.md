[![Ansible-lint rules explanation][ansible-lint]](https://ansible-lint.readthedocs.io/en/latest/default_rules.html)

[ansible-lint]: https://img.shields.io/badge/Ansible--lint-rules%20table-blue.svg


# Ansible Role: nfdump and nfsen-ng

An Ansible Role that installs nfdump and nfsen-ng on Debian.

## Requirements

* ansible:2.10
## Role Variables

### Full

*ready to use*

```yaml
---
# defaults file for matiferrigno.ansible-nfsen-ng


#############################################
# extras
#   installs apache2-php, ntp/chrony and git
#############################################

nfsen_install_ntp: true
nfsen_install_apache_php: true
nfsen_install_git: true

#############################################
# nfsen-ng 
#   web interface
#############################################

# source repo
nfsen_gitrepo: https://github.com/mbolli/nfsen-ng
nfsen_documentroot: /var/www/nfsen-ng
nfsen_servername: nfsen-ng.local
nfsen_log: LOG_DEBUG # LOG_INFO... (just priority, always goes to syslog)
nfsen_ports: # combobox ports
  - 80
  - 443
  - 53
  - 22
nfsen_default_profile: "{{ nfdump_name }}" # set default profile

#############################################
# nfdump 
#   compile, install and configure
#   nfcapd services
#############################################

# compilation
nfdump_gitrepo: https://github.com/phaag/nfdump.git
nfdump_version: v1.6.23
nfdump_fromsources: true
nfdump_bins: /usr/local/bin

# services

# just one service
nfdump_pid: /var/run/nfcapd.pid
nfdump_port: 2055
nfdump_name: default
nfdump_dumproot: /var/nfdump

# 1 or more services
nfdump_sources:
  - name: borde
    port: 2055
  - name: test
    port: 2056

```

## Example Playbook


```yaml
    - hosts: nfsen-ng-server
      roles:
         - { role: matiasferrigno.nfsen-ng }
```

## Testing

### Requirements

  * molecule
  * podman or vagrant/vbox

```
$ molecule check -s vagrant
```

or

```
$ molecule check -s podman
```

## TODO

...

## License


MIT / BSD

## Author Information


This role was created in 2021 by Matías Emanuel Ferrigno.