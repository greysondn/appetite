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
memory:
    -
        # example taken from Super Mario World (SNES)
        name: player_powerup
        domain: WRAM
        address: 0x7E0019
        format: int
        length: 1
        byte_order: little
        values:
            default: "unknown"
            small: 0
            big:   1
            cape:  2
            fire:  3
```

# Field Definitions

## `name`

```yaml
type:                 string
default:              n/a
is_required:          true
must_be_unique:       true
given_to:
    archipelago: false
    bizhawk:     false
```

The name used for this variable. This is also used as a primary key elsewhere in APpetite.

In general, where a variable is explicitly named (mostly PC games), the variable name should match that to help ease implementation.

## `domain`

```yaml
type:                 string
default:              "main"
is_required:          false
must_be_unique:       false
given_to:
    archipelago: false
    bizhawk:     true
```

The memory domain this value exists in.

Whether this is required and the valid values for it will be platform-dependent.

## `address`

```yaml
type:                 string
default:              "main"
is_required:          false
must_be_unique:       false
given_to:
    archipelago: false
    bizhawk:     true
```

The memory address this value exists in, ostensibly (and probably actually) in `domain`.

Whether this is required and the valid values for it will be platform-dependent.

## `format`

```yaml
type:                 string
default:              "bytes"
is_required:          true
must_be_unique:       false
given_to:
    archipelago: false
    bizhawk:     false
```

The core format for this  value.

TODO: List of implemented formats and their meaning. (NB: No formats are implemented as of the writing of this documentation.)

## `length`

```yaml
type:                 unsigned_integer
default:              n/a
is_required:          true
must_be_unique:       false
given_to:
    archipelago: false
    bizhawk:     false # ?
```

The length of this value, in bytes.

## `byte_order`

```yaml
type:                 string
default:              "little"
is_required:          false
must_be_unique:       false
given_to:
    archipelago: false
    bizhawk:     false
```

The byte order for this value.

This is the normal, conventional meaning for this value. Your valid options are `little` and `big`, and `little` is assumed if you don't write it (as we're dealing with processor addressed memory in most cases).

## `values`

```yaml
type:                 dict[str, Any]
default:              {default: "unknown"}
is_required:          false
must_be_unique:       false
given_to:
    archipelago: false
    bizhawk:     false
```

A mapping of aliases to values. This lets the user shorthand values to something more conventional, as an effort in eliminating magic values.

!!! greysondn "Couldn't Figure It Out"

    At the present time, where the value type for the field is `string`, I cannot see any way to make this work. Sorry. Just write your string, the value should be semantic anyway?

The keys must be strings, and there must be a default key which relates to what is returned if a value has no matching key.

You can also just use the raw values, this isn't trying to tie your hands up, it's just trying to be helpful.
