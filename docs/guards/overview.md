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
# ... some field which requires a guard...
# ... and then, indented to the correct depth...
guard:
    type: and
    params:
        next:
            - type: always
            - type: has_item
              params:
                  name: Potato
                  count: 1
            - type: memory_equals
              params:
                  name: player_powerup
                  value: fire
            - type: or
              params:
                  next:
                      - type: always # contrived, granted
```

# Guard Types

## `always`

### Summary

Always returns `true`.

 The default guard for all circumstances, used when none is defined.

### Example

```yaml
guard:
    type: always
```

### Parameters

None.

## `and`

### Summary

A guard used for compositional purposes.

Lazily evaluates its children to return it's value. If all children return `true`, this returns `true`; if any child returns `false`, this returns `false`.

### Example

```yaml
guard:
    type: and
    params:
        next:
            -
                type: always
```

### Parameters

#### `next`

A list of guards. The effective children of this guard that it's to evaluate.

## `has_item`

### Summary

Checks whether the player has a given item based on the game state representation. ***This doesn't necessarily mean an item in the actual underlying game.***

### Example

```yaml
guard:
    type: has_item
    params:
        name: Potato
        count: 8999
```

### Parameters

#### `name`

The name of the item in the game state representation. Should match the `name` value defined in the [items file](../items/overview.md).

#### `count`

Optional. The count of the item the player would have to have, at minimum. Unsigned integer. The default is `1` if not specified.

## `memory_equals`

### Summary

Checks that a memory address is equal to some expected value.

### Example

```yaml
guard:
    type: memory_equals
    params:
        name: player_powerup
        value: fire
```

### Parameters

#### `name`

The name defined in the [memory map file](../memory_map/overview.md).

#### `value`

The value the memory address must be equal to. Either a key defined in `values` from the [memory map file](../memory_map/overview.md) or an exact value.

## `memory_greater_than`

### Summary

Checks that a memory address is greater than some expected value.

### Example

```yaml
guard:
    type: memory_greater_than
    params:
        name: player_health
        value: 50
```

### Parameters

#### `name`

The name defined in the [memory map file](../memory_map/overview.md).

#### `value`

The value the memory address must be greater than. Either a key defined in `values` from the [memory map file](../memory_map/overview.md) or an exact value.

## `memory_greater_than_or_equals`

### Summary

Checks that a memory address is greater or equal to some expected value.

### Example

```yaml
guard:
    type: memory_greater_than_or_equals
    params:
        name: player_health
        value: 50
```

### Parameters

#### `name`

The name defined in the [memory map file](../memory_map/overview.md).

#### `value`

The value the memory address must be greater than or equal to. Either a key defined in `values` from the [memory map file](../memory_map/overview.md) or an exact value.

## `memory_less_than`

### Summary

Checks that a memory address is less than some expected value.

### Example

```yaml
guard:
    type: memory_less_than
    params:
        name: player_health
        value: 50
```

### Parameters

#### `name`

The name defined in the [memory map file](../memory_map/overview.md).

#### `value`

The value the memory address must be less than. Either a key defined in `values` from the [memory map file](../memory_map/overview.md) or an exact value.

## `memory_less_than_or_equals`

### Summary

Checks that a memory address is less or equal to some expected value.

### Example

```yaml
guard:
    type: memory_less_than_or_equals
    params:
        name: player_health
        value: 50
```

### Parameters

#### `name`

The name defined in the [memory map file](../memory_map/overview.md).

#### `value`

The value the memory address must be less than or equal to. Either a key defined in `values` from the [memory map file](../memory_map/overview.md) or an exact value.


## `memory_not_equals`

### Summary

Checks that a memory address is not equal to some expected value.

### Example

```yaml
guard:
    type: memory_not_equals
    params:
        name: player_powerup
        value: fire
```

### Parameters

#### `name`

The name defined in the [memory map file](../memory_map/overview.md).

#### `value`

The value the memory address must not be equal to. Either a key defined in `values` from the [memory map file](../memory_map/overview.md) or an exact value.

## `or`

### Summary

A guard used for compositional purposes.

Lazily evaluates its children to return it's value. If all children return `false`, this returns `false`; if any child returns `true`, this returns `true`.

### Example

```yaml
guard:
    type: or
    params:
        next:
            -
                type: always
```

#### `next`

A list of guards. The effective children of this guard that it's to evaluate.

