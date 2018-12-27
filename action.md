![logo](./img/icon.png)

# Action

The `foreman` supports multiple script engines such as Python and LUA, and so the developer can define the action methods using your favorite programming languages.

## Function Format

The `foreman` supports any programming languages to define the actions, but any actions must conform to the following function format.

```
bool function_name(params, results)
```

The `function_name` must be equals to the action name which is specified in the [FQL](./dsl.md).

The function can get input parameters which are passed from the source object in the route from the `params` dictionary, it should return the result to the `results` dictionary. The `param` and `results` are dictionary objects in the programming language. The output results are passed into the input parameters of the next destination object.

The function should return a `true` when it can execute the action normally, otherwise `false`.

### Example

The following code shows an example to define an echo action in Python.

```
def foreman_echo(params,results):
	for key, value in params.iteritems():
		results[key] = value
	return True
```

The `params` and `results` are [dictionary object](https://docs.python.org/3.6/tutorial/datastructures.html#dictionaries) in Python. The function copies all items from the input `params` to the output `results` simply, and returns `True`.

## Supported Programming Languages

- [Python](action/python_engine.md)
- [System (Shell)](action/system_engine.md)
- LUA
