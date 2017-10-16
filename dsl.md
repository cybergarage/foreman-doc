![logo](./img/icon.png)

# Foreman Query Language 

Foreman supports a domain specific language, Foreman Query Language (FQL), to execute the operator requests. Forman has the HTTP interface to handle the FQL queries.

The operator can post the FQL query to the HTTP interface using GET or POST methods.
FQL, Foreman Query Language.

## Static Methods

Foreman supports .

| Type | Name | Description |
| --- | --- | --- |
| Action | SET | Set a new script method |
| | REMOVE | Remove a specified method |
| Route | SET | Set a new route |
| | REMOVE | Remove a specified route |

## Action

### SET ACTION

The set_method method sets a new method into the local node.

#### Parameters

```
SET ACTION name language encoding code

name     = "name" ":" TOKEN
language = "language" ":" supported-language
encoding = "encoding" ":" ("none" | "base64")
code     = "code" ":" TOKEN

supported-language = ("js" | "java" | "tcl" | "lua")
```

#### Return values

The method doesn't return anything when the method is success, otherwise returns an error object.

### REMOVE ACTION

The remove_method method removes a specified method from the local node.

#### Parameters

```
REMOVE ACTION name

name     = "name" ":" TOKEN
```

##### Return values

The method doesn't return anything when the method is success, otherwise returns an error object.


## Route

#### set_route

The set_route method sets a new route into the local node.

##### Parameters

```
SET ROUTE source destnation [name] [type] [cond] [params]

name       = "name"   ":" TOKEN
source     = "src"    ":" source-object
destnation = "dest"   ":" destnation-object
type       = "type"   ":" ("pipe" | "event")
cond       = "cond"   ":" JS_SCRIPT
params     = "params" ":" "{" *(param) "}"

source-object     = (trigger-name | method-name)
destnation-object = [cluster "."] [node "."] (method-name)
cluster           = ("local" | cluster-name)
node              = ("local" | "all" | "*" | hash-code)
cluster-name      = TOKEN
hash-code         = NODE_HASH
trigger-name      = TOKEN
method-name       = TOKEN

param                      = dest-in-param-name ":" dest-in-param-value-script
dest-in-param-name         = TOKEN
dest-in-param-value-script = JS_SCRIPT
```

##### Return values

The set_route method doesn't return anything when the method is success, otherwise returns an error object.

#### remove_route

The remove_route method removes a specified route from the local node.

##### Parameters

```
SET ROUTE name | (source destnation)

name       = "name"   ":" TOKEN
source     = "src"    ":" source-object
destnation = "dest"   ":" destnation-object

source-object     = (trigger-name | method-name)
destnation-object = [cluster "."] [node "."] (method-name)
cluster           = ("local" | cluster-name)
node              = ("local" | "all" | "*" | hash-code)
cluster-name      = TOKEN
hash-code         = NODE_HASH
trigger-name      = TOKEN
method-name       = TOKEN
```

##### Return values

The remove_route method doesn't return anything when the method is success, otherwise returns an error object.
