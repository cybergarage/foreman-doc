![foreman_logo](./img/icon.png)

# Configuration

`foremand` is a deamon command of [Foreman](https://github.com/cybergarage/foreman-doc/), and it can specify a configuration TOML file.

## Command Line Options

`foremand` supports the following command line options.

```
SYNOPSIS
foremand [OPTIONS]

Logs to stdout by default, can be changed in the config file.

OPTIONS
-config : Path to a configuration file.
-query  : Path to a query file.
-v      : Enable verbose output.

RETURN VALUE
  Return EXIT_SUCCESS or EXIT_FAILURE
```

See [foremand.go](https://github.com/cybergarage/foreman-go/blob/master/foremand/foremand.go) in [foreman-go](https://github.com/cybergarage/foreman-go/) directly to know the latest specification.

## Configuration Properties

`foremand` can specify a configuration file based on [TOML](https://github.com/toml-lang/toml) format as the following.

```
[Log]
file = "/var/log/foreman/foremand.log"
level = "INFO"

[Server]
Cluster = "foreman"
Host = "localhost"
HTTPPort = 8188
CarbonPort = 2003
ConnectionTimeout = 60
Finder = "echonet"

[FQL]
#Path = "/fql"
#Query = "q"

[Metrics]
Store = "sqlite"
Interval = 300
Period = 3600

[Bootstrap]
query = <filename> | <directory name> 
```

See [foremand.conf](https://github.com/cybergarage/foreman-go/blob/master/debian/foremand.conf) in [foreman-go](https://github.com/cybergarage/foreman-go/) directly to know the latest specification.

### Bootstrap

#### query

The specfied file name or directory name are loaded after the `foremand` is started or restarted.
The specified file must include only [FQL](dsl.md) strings each line, and `foremand` executes all queries before the node is activated. 
If a directory is specified for the field, `foremand` search the files whose extension are `*.fql` in the directory and load the found query files all.
