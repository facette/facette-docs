---
title: Configuration
description: Configuration of Facette time series data visualization software
menu:
  main-0_4:
   weight: 30
keywords:
- back-end
- backend
- configuration
- documentation
- driver
- facette
- front-end
- log
- mysql
- postgresql
- settings
- socket
- sqlite
- syslog
- tcp
- unix
- yaml
version: "0.4"
---

# Configuration

The configuration file uses [YAML](http://yaml.org/) format and is provided to the service with the `-c` argument. If
not specified, Facette will look for the `/etc/facette/facette.yaml` file.

For a complete example configuration file, see
[facette.yaml](https://raw.githubusercontent.com/facette/facette/master/docs/examples/facette.yaml).

## Main Settings

| Key                   | Type   | Default           | Description                                                                                                 |
|:----------------------|:------:|:------------------|:------------------------------------------------------------------------------------------------------------|
| `listen`              | string | `localhost:12003` | Socket to listen on (use `unix:/path/to/facette.sock` for UNIX socket)                                      |
| `socket_mode`         | string |                   | UNIX socket file mode (e.g. `0400`)                                                                         |
| `socket_user`         | string |                   | UNIX socket file owner (e.g. `facette`)                                                                     |
| `socket_group`        | string |                   | UNIX socket file group (e.g. `facette`)                                                                     |
| `graceful_timeout`    | int    | `30`              | Timeout before forcefully shutdown remaining connections                                                    |
| `root_path`           | string |                   | Root path behind which the service is located (e.g. `/facette`)                                             |
| `log_path`            | string |                   | Logging file path (if `-` logging goes to *stdout*; if empty file logging is disabled)                      |
| `log_level`           | string | `info`            | File logging level (`error`, `warning`, `notice`, `info` or `debug`)                                        |
| `syslog_level`        | string |                   | Syslog logging level (`error`, `warning`, `notice`, `info` or `debug`; if empty syslog logging is disabled) |
| `syslog_facility`     | string | `daemon`          | Syslog logging [facility](https://en.wikipedia.org/wiki/Syslog#Facility))                                   |
| `syslog_tag`          | string | `facette`         | Syslog logging tag                                                                                          |
| `syslog_address`      | string |                   | Syslog logging server address (if empty, host-local logging is performed)                                   |
| `syslog_transport`    | string | `udp`             | Syslog logging network transport protocol (`tcp`, `udp` or `unix`)                                          |
| `backend.driver`      | string | `sqlite`          | Back-end storage driver name (`sqlite`, `pgsql` or `mysql`)                                                 |
| `backend.*`           |        |                   | *See "Back-end Settings" below for details*                                                                 |
| `frontend.enabled`    | bool   | `true`            | Front-end activation flag                                                                                   |
| `frontend.assets_dir` | string |                   | Front-end assets directory path (not used when compiling with builtin assets)                               |
| `default_time_range`  | string | `-1h`             | Default time range for plots retrieval                                                                      |
| `hide_build_details`  | bool   | `false`           | Prevent build details from being exposed in API                                                             |
| `read_only`           | bool   | `false`           | Read-only flag, preventing modifications through API calls                                                  |

## Back-end Settings

### SQLite

| Key            | Type   | Default | Description               |
|:---------------|:------:|:--------|:--------------------------|
| `backend.path` | string | data.db | SQLite database file path |

### PostgreSQL

| Key                | Type   | Default   | Description              |
|:-------------------|:------:|:----------|:-------------------------|
| `backend.host`     | string | localhost | PostgreSQL host address  |
| `backend.port`     | int    | 5432      | PostgreSQL host port     |
| `backend.dbname`   | string | facette   | PostgreSQL database name |
| `backend.user`     | string | facette   | PostgreSQL user name     |
| `backend.password` | string |           | PostgreSQL user password |

### MySQL

| Key                | Type   | Default   | Description         |
|:-------------------|:------:|:----------|:--------------------|
| `backend.host`     | string | localhost | MySQL host address  |
| `backend.port`     | int    | 3306      | MySQL host port     |
| `backend.dbname`   | string | facette   | MySQL database name |
| `backend.user`     | string | facette   | MySQL user name     |
| `backend.password` | string |           | MySQL user password |
