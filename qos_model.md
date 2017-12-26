![logo](./img/icon.png)

# System Model

Foreman consider a distributed system consisting of a finite set of n environments `E = {E1,E2,...,En}` and a finite set of n processes `P = {P1, P2, ..., Pn}` which runs on the environments.

![system model](./img/qos_model.png)

System Metrics. There are a finite set of n environment metrics `Em = {Em1, Em2, ..., Emn}` on the each environment, and a finite set of n process metrics `Pm = {Pm1,Pm2,...,Pmn}` on the each process.

Foreman consider that `Em` and `Pm` are independent each other, there is no direct relationship between `Em` and `Pm`.

# QoS Definition

Foreman consider QoS from the viewpoint of user and operator because the user interested only in the QoS metrics of their service and the operator interested in the QoS metrics of the system and network resources.

Foreman view a service, `S`, as a subset of `P (S ⊂ P)`, and the QoS, Q, is defined as union of a subset of `Pm (QPm ⊂ Pm)` and a subset of `Em (QEm ⊂ Em)`. Q is defined as a union of `QPm` and `QEm`.

## QoS Metrics Object

Foreman consider that user and operator of a service are conscious only metrics of `QPm` or `QEm` to specify their QoS.

Foreman consider that the user specify their QoS only `QPm` and they doesn’t specify metrics of `QEm` directly too because `QEm` is not service level metrics. Similarly, Foreman consider that the operator specify their `QoS` only `QEm`.

## QoS Formula

`Q` is defined the combination of process metrics in Pm which are related to SLA directly, and the each literal can be specified a condition that is true. The combination is represented as an ANF, Algebraic Normal Form.
For example, a QoS is defined as the following:

```
((Pm1 > 1.0) | ((Pm2 = 5)) & ((Pm3 > 2.0) | (Pm4 <= 1))
```

Then the first specified ANF is modified and optimized using the other concerned process and environment metrics with the specified strategy automatically and dynamically.

## QoS EBNF

Currently, QoS should be specified by CNF, Conjunctive Normal Form.

```
qos :=　"(" clause ("&" clause)* ")"
clause := quority ("|" quority)*
quority := "(" var operator value ")"
operetor := "=" | "!=" | ">" | "<" | ">=" |  "<="
var := [a-z_-.]*
value := <floating_point>
```
