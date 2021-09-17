# YAML

Updated for version 4.0.

## YAML Class

_Added in version 4.0_

A class used to parse YAML strings into tables. Great for localization \(compared to JSON\).

Taken from [https://github.com/exosite/lua-yaml](https://github.com/exosite/lua-yaml) The code is sligthly modified but generally function names are the same.

## Functions

| Function | Return type | Description |
| :--- | :--- | :--- |
| eval\(String str\) | Table | Converts a YAML string data to a table |
| dump\(Any value, Number indent\) | String | Returns YAML dump of a value with `indent` as the indentation number |

