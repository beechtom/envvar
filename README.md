# Environment Variable Plugin

This module includes an environment variable plugin for bolt. This allows you to load
values from environment variables in an inventory file or when configuring plugins in
a configuration file.

## Usage

### `envvar::resolve_reference`

The `resolve_reference` task loads values from environment variables for use in an
inventory file or when configuring plugins in a configuration file.

#### Parameters

- `var`: The environment variable to load.

## Examples

Use the `envvar::resolve_reference` task to load a private key into an inventory file:

```
$ export PRIVATE_KEY=bolt
```

```
---
targets:
  - target1.example.com
  - target2.example.com
config:
  ssh:
    private-key:
      key-data:
        _plugin: envvar
        var: PRIVATE_KEY
```

Use the `envvar::resolve_reference` task to load a password and configure another
plugin:

```
$ export VAULT_PASSWORD=bolt
```

```
plugins:
  vault:
    auth:
      method: userpass
      user: bolt
      password:
        _plugin: envvar
        var: VAULT_PASSWORD
```
