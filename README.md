# Percona Client

This role installs the client programs that connect to
[Percona Server](http://www.percona.com/software/percona-server) which is an
enhanced, drop-in MySQL replacement. The role installs the Percona-maintained
APT repository, creates the basic configuration directories, and installs the
basic client programs including:

* `mysql`
* `mysqladmin`
* `mysqlcheck`
* `mysqldump`
* `mysqlimport`
* `mysqlshow`
* `mysqlslap`

## Requirements

This role requires [Ansible](http://www.ansibleworks.com/) version 1.4 or higher
and the Debian/Ubuntu platform.

## Role Variables

The variables that can be passed to this role and a brief description about
them are as follows (additional variables are available in the source):

```yaml
# Enable UTF-8 character set as default
mysql_utf8: true

# Any valid option that can be added to the [client] group of an option file.
# http://dev.mysql.com/doc/refman/5.6/en/mysql-command-options.html
mysql_client:
  port: 3306
  socket: '/var/run/mysqld/mysqld.sock'

# Any valid option that can be added to the [mysqld_safe] group of an option file.
# http://dev.mysql.com/doc/refman/5.6/en/mysqld-safe.html
mysql_mysqld_safe:
  socket: '/var/run/mysqld/mysqld.sock'
  nice: 0

# Any valid option that can be added to the [mysqld] group of an option file.
# http://dev.mysql.com/doc/refman/5.6/en/mysqld.html
mysql_mysqld:
  user: 'mysql'
  port: 3306
  pid-file: '/var/run/mysqld/mysqld.pid'
  socket: '/var/run/mysqld/mysqld.sock'
  basedir: '/usr'
  datadir: '/var/lib/mysql'
  tmpdir: '/tmp'
  lc-messages-dir: '/usr/share/mysql'

# Any valid option that can be added to the [mysqldump] group of an option file.
mysql_mysqldump:
  quick: ~
  quote-names: ~
  max_allowed_packet: '16M'

# Any valid option that can be added to the [isamchk] group of an option file.
mysql_isamchk:
  key_buffer: '16M'
```

## Examples

1) Install Percona client programs with defaults

    ```yaml
    ---
    # This playbook installs Percona client

    - name: Apply Percona client to all db nodes
      hosts: db_clients
      roles:
        - percona
    ```

2) Install Percona client programs with custom variables

    ```yaml
    ---
    # This playbook installs Percona client

    - name: Apply Percona client to all db nodes
      hosts: db_clients
      roles:
        - { role: percona,
            mysql_client:
              port: 3306
          }
    ```

## Dependencies

None.

## License

MIT.
