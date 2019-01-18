![logo](./img/icon.png)

# Action

The `foreman` supports multiple script engines such as Python and LUA, and so the developer can define the action methods using your favorite programming languages such as Python and LUA.

## Action Function

The `foreman` supports any programming languages to define the actions, but any actions must conform to the following function format.

```
bool function_name(params, results)
```

The `function_name` must be equals to the action name which is specified in the [FQL](./dsl.md).

The function can get input parameters which are passed from the source object in the route from the `params` dictionary, and it should return the result to the `results` dictionary. The `param` and `results` are dictionary objects in the programming language. The output results are passed into the input parameters of the next destination object.

The function should return a `true` when it can execute the action normally, otherwise `false`.

## Supported Programming Languages

- [Python](action/python_engine.md)
- [System (Shell)](action/system_engine.md)
- [LUA](action/system_engine.md)

