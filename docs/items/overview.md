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
-
    name: Victory
    virtual: false
    internal: false
    count: 1
    categories:
        - progression
    aliases: []
    groups:
        - Goal Items
    callbacks:
        on_receive:
            name: complete_game
            params:
                pass: true
```

# Field definitions

## `name`

```yaml
type:                 string
default:              n/a
is_required:          true
must_be_unique:       true
given_to_archipelago: true 
```

The name used for this item. This is also used as a primary key elsewhere in
appetite.

## `virtual`

```yaml
type:                 boolean
default:              false
is_required:          false
must_be_unique:       false
given_to_archipelago: unknown
```

TODO: description.

## `internal`

```yaml
type:                 boolean
default:              false
is_required:          false
must_be_unique:       false
given_to_archipelago: unknown
```

TODO: description.

## `count`

```yaml
type:                 unsigned_integer
default:              1
is_required:          false
must_be_unique:       false
given_to_archipelago: indirectly
```

The count of this item to put into the item pool by default. You're always
welcome to override it programmatically.

## `categories`

```yaml
type:                 list[string]
default:              n/a
is_required:          true
must_be_unique:       false
given_to_archipelago: true
```

A list of item categories - in archipelago terms - this item belongs to.

This is possible to get wrong and break the generation, so be sure you know
what you're doing.

The most relevant reference is the `ItemClassification` class in
`BaseClasses.py` in the archipelago source code, [here][ap-src-baseclasses]

However, here is a list of exactly the ones we specifically expect and what they
mean (taken largely from the referenced AP docs). Where relevant, you can (and
should!) use more than one at a time if AP accepts them:

### filler
aka trash, as in filler items like ammo, currency, etc

### progression
Item that is logically relevant. AP protects this item from being placed
on excluded or unreachable locations.

!!! greysondn "Progression Items"
    These are the items that actually let you make progress and reach new
    locations in your game. Typically it's a tool, skill, or a key item.

### useful
AP protects this item from being placed on excluded or unreachable locations.

When combined with another flag like "progression", it means "an especially
useful progression item".

### trap
Item that is detrimental in some way.

### skip_balancing
Item that is logically relevant, but progression balancing should not touch.

Possible reasons for why an item should not be pulled ahead
by progression balancing:

1. This item is quite insignificant, so pulling it earlier doesn't
   help (currency/etc.)

2. It is important for the player experience that this item is evenly
   distributed in the seed (e.g. goal items)

### deprioritized

Should technically never occur on its own.

AP will not be consider for priority locations, unless Priority Locations Fill
runs out of regular progression items before filling all priority locations.

Should be used for items that would feel bad for the player to find on a
priority location. Usually, these are items that are plentiful or
insignificant.

## `aliases`

```yaml
type:                 list[string]
default:              []
is_required:          false
must_be_unique:       false
given_to_archipelago: true
```

A list of alternate names to give this item. Mostly used for hinting.

## `groups`

```yaml
type:                 list[string]
default:              []
is_required:          false
must_be_unique:       false
given_to_archipelago: true
```

A list of item groups to put this item into. This list is given to Archipelago.

!!! greysondn "Player QoL for Hinting"
    When you hint an item group, Archipelago gives you the first unhinted item
    from that group in the logical progression it expects for the solution it
    planned.

    What this means is that it would be nice for your players if you were to
    create, at minimum, two key groups: `Progression` and (if relevant)
    `MacGuffin`.

## `callbacks`

```yaml
type:                 dictonary[string, Any]
default:              []
is_required:          false
must_be_unique:       false
given_to_archipelago: false
```

Todo: Documentation

[ap-src-baseclasses]: https://github.com/ArchipelagoMW/Archipelago/blob/main/BaseClasses.py