![logo](./img/icon.png)

# Data Model

Foreman has two abstracted data models, the registry store and metric store, internally. The registry store is used to store any metadata such as the configuration settings, and the metric store is used to store time-series metrics data such as monitoring data.

![logo](./img/foreman_datamodel.png)

## Registry Store

Foreman has an abstracted registry store to store any metadata such as the configuration settings. The store is a hierarchical key-value store as the following.

![logo](./img/datamodel_registry.png)

The following metadata are stored into the registry store.

- [Programmng Model](programming_model.md)
  - QoS
  - Action
  - Rule
- [Configuration](configuration.md)

### Abstract Interface

The abstracted registry store is defined as the following interface.

```
type Store interface {
	Open() error
	Close() error

	SetRegistry(r *Record) error
	GetRegistry(key string) (*Record, error)
	
	Query(q *Query) ([]*Record, error)

	String() string
}
```

## Metric Store

Foreman has an abstracted metric store to store time-series metrics data such as monitoring data. The store is a simple matrix time-series database as the following.

![logo](./img/datamodel_metrics.png)

### Public Interfaces

Foreman offers the following interfaces to store and access the time-series metrics data in the metric store.

- [RPC Protocol](rpc_protocol.md)
  - [Foreman Query Language](dsl.md)
- [Graphite Compatible Interface](graphite.md)


### Abstract Interface

The abstracted metric store is defined as the following interface.

```
type Store interface {
	SetRetentionInterval(value time.Duration) error
	GetRetentionInterval() (time.Duration, error)

	Open() error
	Close() error

	AddMetric(m *Metric) error
	Query(q *Query) (ResultSet, error)

	String() string
}
```
