![logo](./img/icon.png)

# RPC Protocol

Foreman offers the following RPC (Remote Procedure Call) protocol to execute FQL, [Foreman Query Language](dsl.md), over HTTP.

## The Query API

`foreman` provies a `/fql` endpoint for quering any [Foreman Query Language](dsl.md) commands.

```
http://<host>:<rpc port>/fql?q=<query>
```

### Response

`foreman` returns a good HTTP status code (200) with the JSON response when the request is executed normally, otherwise a bad HTTP status code with an error JSON response. See [Foreman Query Language](dsl.md) to know the JSON responses in more detail. 

## The Configuration API

`foreman` provies a `/` endpoint for quering the node infomation easily.

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
