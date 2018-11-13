![logo](./img/icon.png)

# RPC Protocol

Foreman offers the following RPC (Remote Procedure Call) protocol to execute FQL, [Foreman Query Language](dsl.md), over HTTP.

## Query

```
http://<host>:<rpc port>/fql?q=<query>
```

### Response




## Configuration

```
http://<host>:<rpc port>/
```

### Response 

`foreman` returns the following configuration response which includes current running settings of the node.

```
{
  "config":{
    "boostrap":0,
    "carbon_port":2003,
    "host":"localhost",
    "http_port":8188, 
    "log_level":"TRACE",
    "metrics_store":"sqlstore/0.8.6",
    "product":"foreman",
    "version":"0.8.5"
  }
}
```
