![logo](../img/icon.png)

# Python

The `foreman` supports Python as a programming languages to define actions in [FQL](./dsl.md), and the action functions are must conform to the following function format.


```
def <function_name>(params,results):
	return <True or False>
````

The `params` and `results` are [dictionary object](https://docs.python.org/3.6/tutorial/datastructures.html#dictionaries) in Python. The function can get input parameters which are passed from the source object in the route from the input `params`, it should return the result to the output `results`. 
The function should return a `True` when it can execute the action normally, otherwise `False`.


## Embedded System Functions

The `foreman` offers the following embedded functions for Python to define complex actions.

| Module | Category | Function | Description |
| --- | --- | --- | --- |
| foreman | Query | execute_query(query) | Posts a query to the local node. |
| | | post_query(host, port, query) | Posts a query to the specified remote node. |
| | Register | set_register(key, value) | Sets the specified key and value into the local register store. |
| | | get_register(key) | Gets a register value of the specified key from the local register store. |
| | | remove_register(key) | Removes the specified register from the local register store. |

### Query

#### foreman.execute_query(query)

The `execute_query` posts a query to the local node.

##### Parameters

| Name | Type | Description |
| --- | --- | --- |
| query | string |  a query string


##### Return values

| Index | Type | Description |
| --- | --- | --- |
| 0 | Dictionary |  Return a json dictionary object of the executed query when the query is executed normally, otherwise None

##### Example

The following code shows how to use the `execute_query` function.

```
import foreman
jsonRes = foreman.execute_query("EXPORT FROM CONFIG")
if jsonRes is not {
  .....
}
```

#### foreman.post_query(host, port, query)

The `post_query` posts a query to the node of the specified host and port.

##### Parameters

| Name | Type | Description |
| --- | --- | --- |
| host | string |  a remote address
| port | int | a remote port
| query | string |  a query string


##### Return values

| Index | Type | Description |
| --- | --- | --- |
| 0 | Dictionary |  Return a json dictionary object of the executed query when the query is executed normally, otherwise None

##### Example

The following code shows how to use the `post_query` function.

```
import foreman
jsonRes = foreman.post_query("localhost", 8188, "EXPORT FROM CONFIG")
if jsonRes is not {
  .....
}
```

### Register

#### foreman.set_register(key, value)


The `set_register` function sets the specified key and value into the local node register.

##### Parameters

| Name | Type | Description |
| --- | --- | --- |
| key | string |  a register key
| value | string | a register value

##### Return values

| Index | Type | Description |
| --- | --- | --- |
| 0 | Boolean |  `True` or `False`

##### Example

The following code shows how to use the `set_register` function.

```
import foreman
key = "m0"
val = "1.0"
ok = foreman.set_register(key, val)
if (ok) {
  .....
}
```

#### foreman.get_register(key)

The `get_register` function returns a register by the specified key from the local node register.

##### Parameters

| Name | Type | Description |
| --- | --- | --- |
| key | string |  a register key

##### Return values

| Index | Type | Description |
| --- | --- | --- |
| 0 | string |  Return a register value when the key exists, otherwise ""

##### Example

The following code shows how to use the `get_register` function.

```
import foreman
key = "m0"
value = foreman.get_register(key);
if (0 < len(value)) {
  .....
}
```

#### foreman.remove_register(key)

The `remove_register` function removes the specified register from the local register store.

##### Parameters

| Name | Type | Description |
| --- | --- | --- |
| key | string |  a register key

##### Return values

| Index | Type | Description |
| --- | --- | --- |
| 0 | Boolean |  `True` or `False`

##### Example

The following code shows how to use the `remove_register` function.

```
import foreman
key = "m0"
ok = foreman.remove_register(key, val)
if (ok) {
  .....
}
```
