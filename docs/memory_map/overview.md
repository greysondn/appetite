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
        default: world
        aliases:
            usa:    world
            europe: world
            japan:  world
        versions:
            world:
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

## `default`

```yaml
type:                 string
default:              n/a
is_required:          true
must_be_unique:       true
given_to:
    archipelago: false
    bizhawk:     false
```

The memory map can specify multiple versions to be selected from. At least one version must be specified, and this must be defined as the default.

In the example memory map, the only version specified is "world", and this is the version that has fields defined. 

!!! greysondn "Helping Developers Help Users"

    You *should* explicitly define your version, then set it as the default if that's your intention. The design choice in separating the two fields is deliberate, as there have been multiple user complaints about only supporting USA or European versions of games in the Archipelago Discord.

    Theoretically, this should let someone come by later and set the fields which match (via aliases or whatever) and also fix the fields which don't match (via explicitly named versions) per version.

    I also have strong feelings about different revisions of games. That's typically out of scope for work like this but would also apply as a possibility to address here.

## `aliases`

```yaml
type:                 dict[string, string]
default:              {}
is_required:          false
must_be_unique:       false
given_to:
    archipelago: false
    bizhawk:     false
```

A dictionary of aliases from one name to another.

Primarily meant to help repoint versions by name without repeating oneself where two versions have the same values otherwise.

An example might be where REV1 and REV2 of a game have some small differences which require specifying but most details are the same. Defining the majority of the memory addresses via alias prevents repetition. Where there are differences, they can then be explicitly specified, and then telling APpetite to initialize for the given revision should be figuratively seamless.

## `versions`

```yaml
type:                 dict[string, dict[]]
default:              n/a
is_required:          true
must_be_unique:       true
given_to:
    archipelago: false
    bizhawk:     false
```

A top level key for the different versions of the memory map data for this named value.

The version string should match the standard version name in some meaningful way.

This is later used - alongside `default` and `aliases` - to pick the data to use when constructing the model of the game's state.

The rest of the fields are per-version (and will be noted as such), and define the version dictionary's shape.

## `domain` (per version field)

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

## `address` (per version field)

```yaml
type:                 uint
default:              0
is_required:          false
must_be_unique:       false
given_to:
    archipelago: false
    bizhawk:     true
```

The memory address this value exists in, ostensibly (and probably actually) in `domain`.

Whether this is required and the valid values for it will be platform-dependent.

## `format` (per version field)

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

## `length` (per version field)

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

## `byte_order` (per version field)

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

## `values` (per version field)

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
