Stouts.influxdb
===========

[![Build Status](http://img.shields.io/travis/Stouts/Stouts.influxdb.svg?style=flat-square)](https://travis-ci.org/Stouts/Stouts.influxdb)
[![Galaxy](http://img.shields.io/badge/galaxy-Stouts.influxdb-blue.svg?style=flat-square)](https://galaxy.ansible.com/list#/roles/1907)

Ansible role which manage [influxdb](http://http://http://hekad.readthedocs.org/)

* Install and configure InfluxDB


#### Variables

Here is the list of all variables and their default values:

```yaml
influxdb_enabled: yes                           # The role is enabled
influxdb_version: latest                        # Set version
influxdb_deb: http://s3.amazonaws.com/influxdb/influxdb_{{influxdb_version}}_amd64.deb

influxdb_root_password: 'root'
influxdb_databases: []                          # Create databases. Ex. [stats, grafana]
influxdb_users: []                              # Create users. Ex. [{ db: name, name: username, password: pass }]

influxdb_bind_address: 0.0.0.0
influxdb_port: 8086
influxdb_admin_port: 8083

influxdb_input_plugins_graphite: {}
influxdb_input_plugins_graphite_default:
  address: "{{influxdb_bind_address}}"
  database: graphite
  enabled: no
  port: 2003
  udp_enabled: no

influxdb_input_plugins_collectd: {}
influxdb_input_plugins_collectd_defaults:
  address: "{{influxdb_bind_address}}"
  database: graphite
  enabled: no
  port: 2003
  typesdb: /usr/share/collectd/types.db

influxdb_input_plugins_udp: {}
influxdb_input_plugins_udp_defaults:
  database: stats
  enabled: no
  port: 4444
```

#### Usage

Add `Stouts.influxdb` to your roles and setup the variables in your playbook file.
Example:

```yaml

- hosts: all

  roles:
    - Stouts.influxdb

  vars:
    influxdb_input_plugins_graphite:
    database: stats
    enabled: yes
    udp_enabled: yes
    influxdb_databases: [stats, grafana]
    influxdb_users: [{ db: stats, name: grafana, pass: grafana }]
    influxdb_users: [{ db: grafana, name: grafana, pass: grafana }]
```

#### License

Licensed under the MIT License. See the LICENSE file for details.

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Stouts/Stouts.influxdb/issues)!
