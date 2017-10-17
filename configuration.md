![foreman_logo](./img/icon.png)

# Configuration

`foremand.toml` is a main configuration file of Foreman.

## Properties

### Server

| Section | Property | Type | Description |
| --- | --- | --- | --- |
| server | http_port | Integer | |
| | carbon_port | Integer | |

### QoS

| Section | Sub Section | Property | Type | Description |
| --- | --- | --- | --- | --- |
| qoses | qos | name | String | |
| | | formula | String | |

### Action

| Section | Sub Section | Property | Type | Description |
| --- | --- | --- | --- | --- |
| actions | action | name | String | |
| | | language | String | python |
| | | encoding | String | |
| | | code | String | |

### Route

| Section | Sub Section | Property | Type | Description |
| --- | --- | --- | --- | --- |
| routes | route | name | String | |
| | | src | String | |
| | | dest | String | |
