![logo](./img/icon.png)

# QoS Action

The action is a programming code for autonomous recovery. Foreman defines the abstract interface, and so the operator can write the action using the following dynamic programming languages.

- Python
- LUA
- System (Shell Command)

## Action Function

The interface of the action function is specified as the following. 

| Item | Type | Description |
| --- | --- | --- |
| Method Name | - |  |
| Request Result | bool |  |
| Request Paramaters | map<string, object> | |
| Response Paramaters | map<string, object> | |
| Error | error | |

However, the shell has support only the method name and request resut.

## Parameter Data Types

| Foreman Type | Go | C++  | Python | LUA | Shell |
| --- | --- | --- | --- | --- | --- |
| Integer | Int64 | long | long | - | - |
| Real | float64 | double | float | - | - |
| String | string | string | string | - | - |
| Bool | bool | bool | bool | - | - |

## Supported Programming Languages

### Python

For Python, the action method specification is bellow.

```
def <method_name>(params, results):
    return ((True || None) or object)
```

#### Arguments

| Name | Direction | Type | Description |
| --- | --- | --- | --- |
| params | IN | Dictionary | Dictionary of input parameters for the action |
| results | OUT | Dictionary | - |

#### Return value

The action method should return `True` or `None` when it is executed normally. 
However, you don't have to return the success objects expressly because all Python functions return the `None` object when these don't use `return`.

The action method should return an error object when it is not executed normally. The action manager translates the error object to a string, set the string as the detail error message.

### LUA

For LUA, the action method specification is bellow.

```
function <method_name>(params)
    return (true || false), results
end
```

#### Arguments

| Name | Direction | Type | Description |
| --- | --- | --- | --- |
| params | IN | Table | Tableof input parameters for the action |
| results | OUT | Table | - |

#### Return value

The action method should return two resutls, `true` or `false` with the table results when it is executed normally. 

### Shell

The action is executed as a system command in the shell.
The action method has no input parameter, the action code is executed directly without the parameters.
