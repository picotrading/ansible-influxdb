influxdb
========

Role which installs and configures InfluxDB. This role doesn't download the
influxdb package. In order to install it, it needs to be put into a repo (see
[`yumrepo`](https://github.com/picotrading/ansible-yumrepo) role for RedHat-based
distros). You can encapsulate this role to do manage the installation of the
package automatically. The configuraton of the role is done in such way that it's
not necessary to change the role for any kind of modification. All can be changed
via parameters used by the role. See examples below.


Example
-------

```
---

# Example of how to use the role with default parameters
- hosts: myhost1
  roles:
    - influxdb

# Example how to customize some of the role parameters
- hosts: myhost2
  roles:
    - role: influxdb
      influxdb_graphite_plugin_enabled: 'true'
      influxdb_graphite_db: grafana

# Or it's possible to change the structure of the template completely
#- hosts: myhost3
#  roles:
#    - role: influxdb
#      # see defaults/main.yaml for example
#      influxdb_config:
#        .
#        ..
#        ...
```


Role variables
--------------

List of variables used by the role:

```
# Default host name
influxdb_hostname: "{{ ansible_hostname }}"

# Default bind address
influxdb_bind_address: 0.0.0.0

# Reporting is disabled by default
influxdb_reporting_disabled: 'true'

# Default loging level [fine|debug|info|warn|error]
influxdb_logging_level: info

# Default log file
influxdb_logging_file: /opt/influxdb/shared/log.txt

# Default admin port number
influxdb_admin_port: 8083

# Default API port number
influxdb_api_port: 8086

# Default API read timeout
influxdb_api_read_timeout: 5s

# Default API configuration block
influxdb_api:
  port: "{{ influxdb_api_port }}"
  read-timeout: "{{ influxdb_api_read_timeout }}"
#  ssl-port = 8084
#  ssl-cert = /path/to/cert.pem

# Graphite input plugin is disabled by default
influxdb_graphite_plugin_enabled: 'false'

# Default Graphite database name
influxdb_graphite_db: graphite

# Default Graphite port number
influxdb_graphite_port: 2003

# Collectd input plugin is disabled by default
influxdb_collectd_plugin_enabled: 'false'

# Default Collectd database name
influxdb_collectd_db: collectd

# Default Collectd port number
influxdb_collectd_port: 25826

# Default Collectd types DB
influxdb_collectd_typesdb: /usr/share/collectd/types.db

# UDP input plugin is disabled by default
influxdb_udp_plugin_enabled: 'false'

# Default UDP database name
influxdb_udp_db: udp

# Default UDP port number
influxdb_udp_port: 4444

# Default udp servers configuration block
influxdb_udp_servers:
  - enabled: 'false'
    port: 5551
    database: db1
#  - enabled: 'false'
#    port: 5552
#    database: db2

# Default raft port number
influxdb_raft_port: 8090

# Default raft directory
influxdb_raft_dir: /opt/influxdb/shared/data/raft

# Raft debugging is disabled by default
influxdb_raft_debug: 'false'

# Default raft election timeout
influxdb_raft_election_timeout: 1s

# Default list of seed servers
influxdb_cluster_seed_servers: []

# Default cluster prtobuf port number
influxdb_cluster_protobuf_port: 8099

# Default cluster protobuf timeout
influxdb_cluster_protobuf_timeout: 2s

# Default cluster protobuf heartbeat time
influxdb_cluster_protobuf_heartbeat: 200ms

# Default cluster protobug min backoff time
influxdb_cluster_protobuf_min_backoff: 1s

# Default cluster protobuf max backoff time
influxdb_cluster_protobuf_max_backoff: 10s

# Default cluster write buffer size
influxdb_cluster_write_buffer_size: 1000

# Default cluster response buffer size
influxdb_cluster_max_response_buffer_size: 100

# Default cluster concurrent shard query limit
influxdb_cluster_concurrent_shard_query_limit: 10

# Default storage directory
influxdb_storage_dir: /opt/influxdb/shared/data/db

# Default storage write buffer size
influxdb_storage_write_buffer_size: 10000

# Default storage engine
influxdb_storage_default_engine: rocksdb

# Defaumt max bunber of open shards
influxdb_storage_max_open_shards: 0

# Default storage point batch size
influxdb_storage_point_batch_size: 100

# Default storage write batch size
influxdb_storage_write_batch_size: 5000000

# Default storage retention swwp period
influxdb_storage_retention_sweep_period: 10m

# Default max number of open files for LevelDB storage engine
influxdb_storage_engines_leveldb_max_open_files: 1000

# Default LRU cache size for LevelDB storage engine
influxdb_storage_engines_leveldb_lru_cache_size: 200m

# Default max number of open files for RocksDB storage engine
influxdb_storage_engines_rocksdb_max_open_files: 1000

# Default LRU cache size for RocksDB storage engine
influxdb_storage_engines_rocksdb_lru_cache_size: 200m

# Default max number of open files for HyperLevelDB storage engine
influxdb_storage_engines_hyperleveldb_max_open_files: 1000

# Default LRU cache size for HyperLevelDB storage engine
influxdb_storage_engines_hyperleveldb_lru_cache_size: 200m

# Default map size for LMDB storage engine
influxdb_storage_engines_lmdb_map_size: 100g

# Default wal directory
influxdb_wal_dir: /opt/influxdb/shared/data/wal

# Default flush after time
influxdb_wal_flush_after: 1000

# Default wal bookmark after time
influxdb_wal_bookmark_after: 1000

# Default wal index after time
influxdb_wal_index_after: 1000

# Default wal request per logfile time
influxdb_wal_requests_per_logfile: 10000
```


License
-------

MIT


Author
------

Jiri Tyr
