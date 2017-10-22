![logo](./img/icon.png)

# Data Model


```
type Store interface {
	Open() error
	Close() error

	SetRegistry(r *Record) error
	GetRegistry(key string) (*Record, error)

	String() string
}
```

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
