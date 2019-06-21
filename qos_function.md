![logo](./img/icon.png)

# QoS Function

The QoS functions are embedded functions which return a value using the specified parameters. 


## ABS

```
ABS(param1)

param1 : <variable> | <number>
```

The `ABS()` returns the absolute value of the specified variable or number, it returns an absolute metrics value [the registry manager](./data_model.md) when the parameter is a variable, otherwise absolute number of the specified number.

## Extending Embedded Functions

To add new embedded function yourself, the function must implement the following `Function::Execute()`.

```
type Function interface {
    Execute([]interface{}) (interface{}, error)
}
```

To implement a new function easily, `foreman-go` offers the following base function which implements other required methods of [foreman/kb/Function](https://github.com/cybergarage/foreman-go/blob/master/foreman/kb/function.go).

- [qos/function/Function](https://github.com/cybergarage/foreman-go/blob/master/foreman/qos/function/function.go)

### Implementing New Embedded Function

For example, the `ABS()` embeds the [Function](https://github.com/cybergarage/foreman-go/blob/master/foreman/qos/function/function.go) to support the [kb/Function](https://github.com/cybergarage/foreman-go/blob/master/foreman/kb/function.go) methods easily, and implement only the `Function::Execute()` as the following.

- [foreman/qos/function/abs.go](https://github.com/cybergarage/foreman-go/blob/master/foreman/qos/function/abs.go)

After the implementation, add the new function into `QoS::CreateFunctionOperand()` to enable it as the following.

- [foreman/qos/qos_factory.go](https://github.com/cybergarage/foreman-go/blob/master/foreman/qos/qos_factory.go)

### Testing New Embedded Function

To test the new embedded functions, the `foreman` scenario test is useful. For example, the `ABS()` is tested in the following scenario test.

- [scenario_qos_function_abs.test](https://github.com/cybergarage/foreman-go/blob/master/test/scenarios/scenario_qos_function_abs.test)

To execute the scenario test, add the scenario test file into the following test file.

- [query_scenario_test.go](https://github.com/cybergarage/foreman-go/blob/master/foreman/query_scenario_test.go)

For the debugging, you should add scenario test file into TestQueryDebuggingScenarios() at first. After you finish the debugging, move it to `TestQueryBasicScenarios()` or `TestQueryPythonActionScenarios()` 
