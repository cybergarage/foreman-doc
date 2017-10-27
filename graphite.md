![foreman_logo](./img/icon.png)

# Graphite

Foreman supports the following compatible interfaces for [Graphite](https://graphiteapp.org).

## Carbon API

Foreman supports only the following plaintext protocol now.

- [Feeding In Your Data](http://graphite.readthedocs.io/en/latest/feeding-carbon.html)

| Function | Support |
|---|---|
| Plaintext Protocol | O |
| Pickle Protocol | X |

## Render API

Foreman supports only the following graphing metrics parameters, and it doesn't support graphing metrics parameters all.

- [The Render URL API](http://graphite.readthedocs.io/en/latest/render_api.html)

| Metrics Parameter | Support | Description
|---|---|---|
| target | O | |
| from | O | |
| util | O | |
| template | X | |
| format | O | json, csv |
| template | O | |
| template | O | |
| template | O | |

### Functions

Foreman supports the following functions or the Render API.

- [Functions](http://graphite.readthedocs.io/en/latest/functions.html)

| Function | Support |
|---|---|
| absolute |  |
| aggregate |  |

