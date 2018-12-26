![logo](./img/icon.png)

# Foreman Query Language 

Foreman supports a domain specific language, Foreman Query Language (FQL), to execute the operator requests. Forman has the HTTP interface to handle the FQL queries.

The operator can post the FQL query to the HTTP interface using GET or POST methods.

## Command Line Tool

`foreman-py` is a client package for Foreman, and it has a command line tool, [`fql`](./doc/fql.md), which can execute FQL easily. Please check the following document to know the tool in more detail.

- [`foreman-py`](https://github.com/cybergarage/foreman-py)
  - [fql - The Foreman Command Line Tool](https://github.com/cybergarage/foreman-py/blob/master/doc/fql.md)

## Overview

FQL supports the following queries.

| Type | Action | Description |
| --- | --- | --- |
| Metrics | SET | Insert a new metrics |
| | SELECT | Get the specified metrics data |
| | ANALYZE | Analyze the specified metrics data |
| | - | - |
| QoS | SET | Set a new QoS formula |
| | EXPORT | Get the specified QoS formula |
| | DELETE | Delete the specified QoS formula |
| | - | - |
| Action | SET | Set a new action |
| | EXPORT | Get the specified action data |
| | DELETE | Delete the specified action |
| | EXECUTE | Execute the specified action |
| | - | - |
| Route | SET | Set a new route |
| | EXPORT | Get the specified route data |
| | DELETE | Delete the specified route |
| | - | - |
| Register | SET | Set a new register data |
| | EXPORT | Get the specified register data |
| | DELETE | Delete the specified register data |
| | - | - |
| Configuration | Export | Export the current all configuration |
| | - | - |

## Metrics

### SET

The method is compatible with the following plaintext protocol of Graphite, it inserts a new metrics.

- [Graphite : Feeding In Your Data](http://graphite.readthedocs.io/en/latest/feeding-carbon.html)

  #### Parameters

```
SET (name, value, timestamp) INTO METRICS

name     = TOKEN
value    = FLOAT
timestamp = UNIX_TIMESTAMP
```

#### Return values

The method doesn't return anything when the method is success, otherwise returns an error object.

### SELECT

The method is compatible with the following Render URL API of Graphite, it returns metrics data of the specified target and period by JSON format.

#### Parameters

```
SELECT (targets)? FROM METRICS (WHERE conditions)?

targets    = ('*' | '(' target (',' target)* ')')
target     = 'name' | 'value' | 'ts'
conditions = condition (AND condition)*
condition  = operand operator operand
operand    = TOKEN
operator   = '<' | '>' | '<=' | '>=' | '==' | '!=' 
```

`SELECT` returns only matched metric names when the target is only specified 'name', otherwise it returns matched metric data which are included with the specified targets such as 'name', 'ts', 'value'.

#### Return values

The method returns the specified metrics data by JSON format. The response is Graphite compatible, and so the metrics response are the following JSON response format when the query targets the metrics data.

- [Graphite : The Render URL API](http://graphite.readthedocs.io/en/latest/render_api.html)

Otherwise, the metrics response are the following JSON response format when the query targets only metrics without data.

- [Graphite : HTTP API](http://graphite-api.readthedocs.io/en/latest/api.html)
  - `/metrics/index.json`

### ANALYZE

The method analyzes the specifid metrics, and it returns the analysys result by JSON format.

#### Parameters

```
ANALYZE METRICS (WHERE condition)?

targets    = ('*' | '(' target (',' target)* ')')
target     = 
condition  = 'name' '==' operand
operand    = TOKEN
```

#### Return values

The method returns the analysis result by JSON format.

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

### EXPORT

The method returns the specified QoS formulas.

#### Parameters

```
EXPORT FROM QOS WHERE (WHERE condition)?

condition  = column operator operand
column    = 'name'
operator   = '=='
operand    = TOKEN
```

#### Return values

The method returns the specified QoS formulas by JSON format. 

### DELETE

The method removes a specified method.

#### Parameters

```
DELETE FROM QOS  (WHERE condition)?

condition  = column operator operand
column    = 'name'
operator   = '=='
operand    = TOKEN
```

##### Return values

The method doesn't return anything when the method is success, otherwise returns an error object.


## Action

### SET

The method sets a new method into the local node. See [Action](./action.md) to define the actions using the supported programming languages.

#### Parameters

```
SET (name, language, code, encoding) INTO ACTION

name     = TOKEN
language = supported-language
code     = TOKEN
encoding = ("none" | "base64")

supported-language = ("js" | "java" | "tcl" | "lua" | "python")
```

#### Return values

The method doesn't return anything when the method is success, otherwise returns an error object.

### EXPORT

The method returns the specified action data.

#### Parameters

```
EXPORT FROM ACTION WHERE (WHERE condition)?

condition  = column operator operand
column    = 'name'
operator   = '=='
operand    = TOKEN
```

#### Return values

The method returns the specified actions by JSON format. 

### DELETE

The remove_method method removes a specified method.

#### Parameters

```
DELETE FROM ACTION  (WHERE condition)?

condition  = column operator operand
column    = 'name'
operator   = '=='
operand    = TOKEN
```

##### Return values

The method doesn't return anything when the method is success, otherwise returns an error object.

### EXECUTE

The method execute a registered method with the specified parameters.

#### Parameters

```
EXECUTE method_name (param_names)? (VALUES param_values)?

method_name   = TOKEN
param_names  = '(' param_name? (',' param_name)* ')'
param_name   = TOKEN
param_values = '(' param_value? (',' param_value)* ')'
param_value = TOKEN
```

#### Return values

The method returns the execution result by JSON format. 

## Route

#### SET

The method sets a new route into the local node.

##### Parameters

```
SET (name, source_name, dest_name) INTO ROUTE

name        = TOKEN
source_name = TOKEN
dest_name   = TOKEN
```

##### Return values

The method doesn't return anything when the method is success, otherwise returns an error object.

### EXPORT

The method returns the specified routes.

#### Parameters

```
EXPORT FROM ROUTE (WHERE condition)?

condition  = column operator operand
column    = 'name'
operator   = '=='
operand    = TOKEN
```

#### Return values

The method returns the specified routes by JSON format. 


#### DELETE

The method removes a specified route.

##### Parameters

```
DELETE FROM ROUTE (WHERE condition)?

condition  = column operator operand
column    = 'name'
operator   = '=='
operand    = TOKEN
```

##### Return values

The method doesn't return anything when the method is success, otherwise returns an error object.

## Register

### SET

The method sets a new register data.

#### Parameters

```
SET (name, data) INTO REGISTER

name    = TOKEN
data  = TOKEN
```

#### Return values

The method doesn't return anything when the method is success, otherwise returns an error object.

### EXPORT

The method returns the specified register data.

#### Parameters

```
EXPORT FROM REGISTER WHERE (WHERE condition)?

condition  = column operator operand
column    = 'name'
operator   = '=='
operand    = TOKEN
```

#### Return values

The method returns the specified register data by JSON format. 

### DELETE

The method removes a specified method from the local node.

#### Parameters

```
DELETE name FROM REGISTER

name     = TOKEN
```
##### Return values

The method doesn't return anything when the method is success, otherwise returns an error object.

## Configuration

### EXPORT

##### Parameters

```
EXPORT FROM CONFIG
```

##### Return values

The method returns the current all configuration properties.

Please see [Configuration](configuration.md) to know the format in more detail.
