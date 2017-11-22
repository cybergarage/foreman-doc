![logo](./img/icon.png)

# Action Model

## Method

Foreman enables to build monitoring actions to define the small methods using any programming languages and connect between the methods like pipeline of Unix.

## Route

Foreman supports dataflow programming as reactive programming to execute a complex DAG (directed acyclic graph). In Foreman, the dataflow function is called as ’route’.

![route](./img/programming_model_route.png)

## Supported Programming Languages

| Item | Type | Description |
| --- | --- | --- |
| Method Name | - |  |
| Request Result | bool |  |
| Request Paramaters | map<string, object> | |
| Response Paramaters | map<string, object> | |
| Error | error | |

### Python

```
def <method_name>(in, out, error):
```

## Event

### QoS

When the QoS manager detects a Qos which is not satisfied, it sends a following event to the specified action method which is a connected with the QoS by the route. 

| Argument | Direction | Type | Description |
| --- | --- | --- | --- |
| qos | IN | QoS |
| - | OUT | - | - |

Currently, Foreman doesn't handle any responses, and so the action method should not return any parameters.
