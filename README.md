# TranClate

A Kotlin library that wraps the whole development process of a Minecraft Bedrock Project and thus provides
a streamlined development experience with

- Autocompletion
- Integrated Documentation
- A debugger that already works in the IDE and gives usefully feedback
- Prevent invalid Code
- The usage of Kotlin as a Tool to minimize Code duplications 

## Concept

The whole concept of TranClate is a [Kotlin DSL](https://kotlinlang.org/docs/type-safe-builders.html) it's intention is
to let the developer only write compilable code, in our case we want to make sure a developer can only write code that
is within the limits of Minecraft. Another goal is to automate everything that can be automated.

````kotlin
addon({
    projectName = "Project Name"
    projectShort = "pn"
    description = "by Timolia Creative"
    packIcon = getResource("general/pack.png")
    world = getResource("world/$worldName")
    version = arrayListOf(1, 0, 0)
}) {
    entity {
        name("id", "Name of The Entity")
        behaviour {
            components {
                damageSensor {
                    trigger {
                        cause = DamageType.ALL
                        dealsDamage = false
                    }
                }
            }
        }
        resource {
            components {
                spawnEgg {
                    eggByColor(Color.RED, Color.BLACK)
                }
            }
        }
    }
}
````

TranClate is also designed to be extended through plugins/libraries. This is 
encouraged through the design desiccation to add/apply data to objects from anywhere.

Example:

```kotlin
//applied by the user
val sampleEntity = entity {
    name("myEntity")
    behaviour {
        components {
            physics()
        }
    }
}

//applied by the plugin
sampleEntity.behaviour {
    components {
        pushable()
    }
}
```

Instead of overwriting the `physics()` component, the second call will apply the `pushable()` components.

With this design plugins/libraries can easily modify predetermined objects like the player entity without
worrying to overwrite code of the developer that is using the plugin/library.
