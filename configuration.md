![foreman_logo](./img/icon.png)

# Configuration

`foremand.toml` is a main configuration file for `foremand`.

## Command Line Options

```
foremand is a deamon command of Forman.

	NAME
	foremand

	SYNOPSIS
	foremand [OPTIONS]

	DESCRIPTION
	foremand is a deamon process to Foreman.

	Logs to stdout by default, can be changed in the config file.

	OPTIONS
	-config : Path to a configuration file.
	-query  : Path to a query file.
	-v      : Enable verbose output.

	RETURN VALUE
	  Return EXIT_SUCCESS or EXIT_FAILURE
```

## Configuration Properties

```
[Log]
file = "/var/log/foreman/foremand.log"
level = "INFO"

[Server]
Cluster = "foreman"
Host = "localhost"
HTTPPort = 8188
CarbonPort = 2003
Finder = "echonet"

[FQL]
#Path = "/fql"
#Query = "q"

[Metrics]
Store = "sqlite"
Interval = 300
Period = 3600
```
