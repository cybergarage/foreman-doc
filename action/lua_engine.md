![logo](../img/icon.png)

# LUA

The `foreman` supports LUA as a programming languages to define actions in [FQL](./dsl.md), and the action functions are must conform to the following function format.


```
def <function_name>(params,results):
	return <true or false>
````

The `params` and `results` are [table object](https://www.lua.org/pil/2.5.html) in LUA. The function can get input parameters which are passed from the source object in the route from the input `params`, it should return the result to the output `results`. 
The function should return a `true` when it can execute the action normally, otherwise `false`.
