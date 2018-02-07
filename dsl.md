![logo](./img/icon.png)

# Foreman Query Language 

Foreman supports a domain specific language, Foreman Query Language (FQL), to execute the operator requests. Forman has the HTTP interface to handle the FQL queries.

The operator can post the FQL query to the HTTP interface using GET or POST methods.

## Overview

FQL supports the following queries.

| Type | Action | Description |
| --- | --- | --- |
| Metrics | SET | Insert a new metrics |
| | SELECT | Get the specified metrics data |
| | - | - |
| QoS | SET | Set a new QoS formula |
| | DELETE | Delete the specified QoS formula |
| | - | - |
| Action | SET | Set a new script action |
| | DELETE | Delete the specified action |
| | - | - |
| Route | SET | Set a new route |
| | DELETE | Delete the specified route |
| | - | - |
| Failure Analysis | ANALYZE | Analyze the specified metrics |
| | - | - |
| Prediction Analysis | ANALYZE | Analyze the specified metrics |
| | - | - |
| Configuration | Export | Export the current all configuration |
| | - | - |

## Metrics

### INSERT

The method is compatible with the following plaintext protocol of Graphite, it inserts a new metrics.

- [Graphite : Feeding In Your Data](http://graphite.readthedocs.io/en/latest/feeding-carbon.html)

#### Parameters

```
SET (id, value, timestamp) INTO METRICS

id     = TOKEN
value    = FLOAT
timestamp = UNIX_TIMESTAMP
```

#### Return values

The method doesn't return anything when the method is success, otherwise returns an error object.

### SELECT

The method is compatible with the following Render URL API of Graphite, it returns metrics data of the specified target and period.

- [Graphite : The Render URL API](http://graphite.readthedocs.io/en/latest/render_api.html)

#### Parameters

```
SELECT (targets)? FROM METRICS (WHERE conditions)?

targets    = ('*' | '(' target (',' target)* ')')
target     = 'id' | 'value' | 'ts'
conditions = condition (AND condition)*
condition  = operand operator operand
operand    = TOKEN
operator   = '<' | '>' | '<=' | '>=' | '==' | '!=' 
```

#### Return values

The method returns the specified metrics data by JSON format.

## QoS

### SET

The method sets a new QoS formula.

#### Parameters

```
SET (name, formula) INTO QOS 

name     = TOKEN
formula  = CNF
```

#### Return values
                     
The method doesn't return anything when the method is success, otherwise returns an error object.

### DELETE

The method removes a specified method from the local node.

#### Parameters

```
DELETE FROM QOS  (WHERE conditions)?

conditions = condition (AND condition)*
condition  = operand operator operand
operand    = TOKEN
operator   = '<' | '>' | '<=' | '>=' | '==' | '!=' 
```

##### Return values

The method doesn't return anything when the method is success, otherwise returns an error object.


## Action

### SET ACTION

The method sets a new method into the local node.

#### Parameters

```
SET ACTION name language encoding code

name     = TOKEN
language = supported-language
encoding = ("none" | "base64")
code     = TOKEN

supported-language = ("js" | "java" | "tcl" | "lua")
```

#### Return values

The method doesn't return anything when the method is success, otherwise returns an error object.

### DELETE ACTION

The remove_method method removes a specified method from the local node.

#### Parameters

```
DELETE FROM ACTION  (WHERE conditions)?

conditions = condition (AND condition)*
condition  = operand operator operand
operand    = TOKEN
operator   = '<' | '>' | '<=' | '>=' | '==' | '!=' 
```

##### Return values

The method doesn't return anything when the method is success, otherwise returns an error object.


## Route

#### SET ROUTE

The method sets a new route into the local node.

##### Parameters

```
SET ROUTE source destnation [name] [type] [cond] [params]

name       = TOKEN
source     = source-object
destnation = destnation-object

source-object     = (qos-name | action-name)
destnation-object = [cluster "."] [node "."] (method-name)
cluster           = ("local" | cluster-name)
node              = ("local" | "all" | "*" | hash-code)
cluster-name      = TOKEN
hash-code         = NODE_HASH
qos-name          = TOKEN
action-name       = TOKEN
```

##### Return values

The method doesn't return anything when the method is success, otherwise returns an error object.

#### REMOTE ROUTE

The method removes a specified route from the local node.

##### Parameters

```
SET ROUTE name | (source destnation)

name       = TOKEN
source     = source-object
destnation = destnation-object

source-object     = (trigger-name | method-name)
destnation-object = [cluster "."] [node "."] (method-name)
cluster           = ("local" | cluster-name)
node              = ("local" | "all" | "*" | hash-code)
cluster-name      = TOKEN
hash-code         = NODE_HASH
trigger-name      = TOKEN
method-name       = TOKEN
```

##### Return values

The method returns the current all configuration properties.

## Failure Analysis

### ANALYZE

The method returns time series related metrics with the specified target for any purposes such as root cause analysis of failures.

##### Parameters

```
ANALYZE CORRELATION target 

target      = TOKEN
```

##### Return values

<TBD>

## Prediction Analysis

### ANALYZE

The method returns time series prediction metrics with the specified target for any purposes such as ....

##### Parameters

```
ANALYZE PREDICTION target 

target      = TOKEN
```

##### Return values

<TBD>

## Configuration

### EXPORT

##### Parameters

```
EXPORT CONFIG
```

##### Return values

The method returns the current all configuration properties.
Please see [Configuration](configuration.md) to know the format in more detail.
