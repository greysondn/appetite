!!! greysondn "Early docs"
    These docs are very early and there's a good chance no matching code exists
    yet. Just so you've been warned.

    Things also are subject to rapid change. Again, you've been warned.


!!! greysondn "Unreferenced"
    The Archipelago docs were not referenced in order to make these docs.

    I've very little doubt something is wrong.
---

[TOC]

---

# Introduction

Okay wait, where's my text

# Example

```yaml
# The data for this example is based on the USA SNES version of Earthbound.
# (It is *not* based on the Earthbound APWorld.)
config:
    presets:
        -  "default"
    settings:
        -
            name: Ness's Name
            help: |
                The first "Don't Care" name for the first hero.
            storage:
                location: config
                key: ness_name
            format:
                type: string
                scheme:
                    length: 6
            values:
                default: Ness
        -
            Name: Evolve Egg
            help: |
                Whether or not to permit eggs to evolve into chicks and later
                chickens.
            storage:
                location: config
                key: evolve_egg
            format:
                type: bool
            values:
                default: True
        -
            Name: Experience Percentage
            help: |
                Percentage of experience fights should be worth, relative to
                vanilla.
            storage:
                location: config
                key: exp_mult
            format:
                type: integer
                scheme:
                    min:    0
                    max: 5000
            values:
                default: 100
        -
            name: Speed multiplier
            help: |
                How fast you walk on the overworld.
            storage:
                location: user_data
                key: walk_speed
                format:
                    type: float
                    scheme:
                        min:  0.1
                        max: 10.0
            values:
                default: 1.0
        -
            name: Starting Character
            help: |
                Character you wish to start with.
            storage:
                location: config
                key: start_character
                format:
                    type: string
                    scheme:
                        length: 6
                        enum: true
                        values:
                            - Ness
                            - Paula
                            - Jeff
                            - Poo
            values:
                default: Ness
```

# Field Definitions

okay wait why are you not writing the docs