# For Apache Cassandra

## Configuration

- [Apache Cassandra : Monitoring¶](http://cassandra.apache.org/doc/latest/operating/metrics.html)
  - [metrics reporter config project](https://github.com/addthis/metrics-reporter-config)

## [CCM (Cassandra Cluster Manager)](https://github.com/riptano/ccm)

### STEP1 : Setup cluster

#### Create and Stop C* Cluseter

```
ccm create foreman -v 3.11.2 -n 1 -s
ccm stop node1
```

### STEP2 : Install option packages

#### Install `metrics-graphite`

- [metrics-graphite](https://mvnrepository.com/artifact/com.yammer.metrics/metrics-graphite)

```
curl -O http://central.maven.org/maven2/io/dropwizard/metrics/metrics-graphite/3.1.5/metrics-graphite-3.1.5.jar
mv metrics-graphite-3.1.5.jar ~/.ccm/repository/3.11.2/lib/
```

### STEP3 : Modify configuration and option

#### `metrics-reporter-config-sample.yaml`

- [metrics-reporter-config-sample.yaml](./tutorial_cassandra_000-conf-001.yml)

#### `jvm.options `

```
# Enable pluggable metrics reporter. See Pluggable metrics reporting in Cassandra 2.0.2.
-Dcassandra.metricsReporterConfigFile=metrics-reporter-config-sample.yaml
 ```

### STEP4 : Start node

 ```
ccm start node1
```

### Note

#### java.lang.NoClassDefFoundError: com/codahale/metrics/graphite/GraphiteSender 

- Install `metrics-graphite`

```
$ tail ~/.ccm/foreman/node1/logs/debug.log
....
INFO  [main] 2018-02-23 13:55:50,524 QueryProcessor.java:163 - Preloaded 0 prepared statements
INFO  [main] 2018-02-23 13:55:50,524 CassandraDaemon.java:349 - Trying to load metrics-reporter-config from file: metrics-reporter-config-sample.yaml
ERROR [main] 2018-02-23 13:55:50,580 CassandraDaemon.java:708 - Exception encountered during startup
java.lang.NoClassDefFoundError: com/codahale/metrics/graphite/GraphiteSender
```
