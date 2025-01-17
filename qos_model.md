![logo](./img/icon.png)

# QoS Model

The knowledge representation for QoS is a human-readable format for autonomous knowledge management. This study manages knowledge based on the rule-based system to separate the static and dynamic rules and actions, and the rules are represented as a common condition format based on Boolean logic. 

## QoS Representation

The QoS knowledge is consist of a QoS formula and the recovery actions. The recovery action is executed when the condition is satisfied. 
The following figure shows the relationship between the conditions and the actions.

![rule](./img/qos_rule.png)

All conditions and actions have their unique names, and the observers can set the behavior of the rule to connect the rule with the actions using the names. This study calls the connection between the rule and the action as a route. The observer can set multiple actions to a rule using multiple routes. 

## QoS Formula

The QoS is defined the combination of process metrics in m which are related to QoS directly, and the each literal can be specified a condition that is true. The combination is represented as an ANF, Algebraic Normal Form.
For example, a QoS is defined as the following:

```
((m1 > 1.0) | ((m2 == 5)) & ((m3 > 2.0) | (ABS(m4) <= 1))
```

Then the first specified ANF is modified and optimized using the other concerned process and environment metrics with the specified strategy automatically and dynamically.

### QoS EBNF

Currently, QoS should be specified by DNF (Disjunctive normal form) as the following EBNF.

```
qos :=　"(" clause ("|" clause)* ")"
clause := formula ("&" formula)*
formula := "(" operand operator operand ")"

operetor := "==" | "!=" | ">" | "<" | ">=" |  "<="
operand := value | variable | function 

value := <integer> | <floating_point>
variable := [a-zA-Z0-9_\-.*]+
function := name "(" (parameter)+ ")"
parameter := value | variable
```

The operand value is a literal such as `1.0` or `10`, and the operand variable is a variable name in [the registry manager](./data_model.md) which stores the latest fed metrics.

The operand functions are embedded functions which return a value using the specified parameters. Please check [QoS Function](./qos_function.md) to know the embedded functions in more detail.

## QoS Action 

Foreman defines the abstract interface, and so the operator can write the action using dynamic programming languages. Foreman support the the following dynamic programming languages.

- Python
- LUA
- System (Shell Command)

See [Action](action.md) to know the specification in more detail.
