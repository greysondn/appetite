!!! greysondn "Early docs"
    These docs are very early and there's a good chance no matching code exists
    yet. Just so you've been warned.

    Things also are subject to rapid change. Again, you've been warned.

---

[TOC]

---

# Introduction

Okay wait, where's my text

# Example

```yaml
# ... some field which requires callbacks...
# ... and then, indented to the correct depth...
callbacks:
    pre_receive:
        type: nop
    on_receive:
        type: write_memory
        params:
            name: player_health
            value: 100
            guard:
                type: always
    post_receive: 
        type: nop
```

# Predefined Callbacks

## `nop`

### Summary

Does nothing. The default callback function for most actions.

### Example

```yaml
callbacks:
    pre_receive:
        type: nop
```

### Parameters

None.

## `write_memory`

### Summary

Writes a value to some address defined in [the memory_map](../memory_map/overview.md).

### Example

```yaml
callbacks:
    on_receive:
        type: write_memory
        params:
            name: player_health
            value: 100
            guard:
                type: always
```

### Parameters

#### `name`

The name given to the memory address in [the memory_map](../memory_map/overview.md).

#### `value`

A value - either by name or by absolute value - that matches the address in [the memory_map](../memory_map/overview.md)

#### `guard`

A valid guard block, as defined in the [guard documentation](../guards/overview.md). Defaults to `always`.