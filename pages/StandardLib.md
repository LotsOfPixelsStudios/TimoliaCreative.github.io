# &#128218; Standard Library

## &#128187; State System

The state system is an abstraction/mix of the animation-controller in the behaviour pack, it's designed to
help write setup function. The advantage is that there is no overhead with entities.

Usage:

````kotlin
stateSystem(addon) {
    identifier = "the_id_of_the_system"
    attachToEntity = "@p"   //you may want to just load the entity that executes the commands to be near the player

    state {
        transitions { transitionNextState(Query.allAnimationsFinished) }
        timeline {
            keyFrame(2f, "/function initial")
            keyFrame(3f, "/say initial finished")
        }
    }

    someList.forEach { it ->
        state {
            transitions {
                transitionNextState(Query.allAnimationsFinished)
            }
            
            timeline {
                keyFrame(1f, "/function some_spec_fun_$it")
                keyFram(2f, "/say $it finished")
            }
        }
    }
    state {
        onStart = arrayListOf("/say finished")
        disposeSystem = true    //make sure all entities only relevant to the system are killed
    }
}
````

Some other useful information and debuting tips: 

````kotlin
stateSystem(addon) {
    attachToEntity = "@p"
    familyType = "state"    //this can be applied at the player so the system is able to ride with this family
    state {
        onEntry = arrayListOf("/say on entry")
        onExit = arrayListOf("/say on exit")

        transitionRaw(2, "1")   //transition to the second state with the query: "1"
        println("Current State: ${this.id}")
    }
    state {
        disposeSystem = true
    }
}
````

You can also trigger a state change with a command: 

````kotlin
stateSystem(addon) {
    //...
}

val command = getStateTransitionCommand(2)  //mc function executable 
````

## &#127918; Player

The standard library provides a way to modify the player within the whole addon without creating
duplicates. But it is still recommended to modify the player in a central file to avoid confusion.

Usage:
````kotlin
val player = Player.modify(addon)

player.modifyBehaviour {
    modifyBehComponents {
        //...
    }
    addAnimController("controller_name") {
        //...
    }
}

player.modifyResource {
    modifyTextures {
        //...
    }
    modifyRenderController {
        //...
    }
}
````

Everything in the player is by standard applied, you have multiple ways to disable certain 
vanilla stuff. 

````kotlin
player.modifyBehaviour {
    modifyBehComponents {
        //disable each component manually
        skipAttack = true
        //or remove all events/components/groups
        removeAllVanillaComponents = true
        removeAllVanillaGroups = true
        removeAllVanillaEvents = true
    }
}
````

## &#128186; Furniture

The standard library provides some presets for furniture, to streamline the process of implementing
new furniture entities.

The presets contain:

- furniture
- lamp
- seatingFurniture
- storageFurniture

each can be called by its name:

````kotlin
furniture("id", "Display Name", addon) {
    texture = getResource("")
    geometry = getResource("")
    height = 1f
    width = 2f
    scale = 1f
    autoRotationAdjustment = true
    
    icon {
        eggByTexture(getResource(""))
    }
    
    //modify more stuff, at this point might consider implementing your own entity
    behaviour {
        components {
            
        }
        componentGroups {
            
        }
        //...
    }
    resource {
        components {
            spawnEgg {}
        }
    }
}
````

## &#128190; Command

### Selector

Call `Selector`, the companion object has all standard selectors, you can select
with the name Annotation like 
````kotlin
val selector = Selector.a
````

or with a more understandable annotation like

````kotlin
val selector = Selector.allPlayers
````

Both Annotations are equivalent and can safely be cast to a string like:

````kotlin
val command = "/tag ${Selector.a} add test"
//or
val selectorString = Selector.a.toString()
````

*Specify selectors:*

To specify what entity we want to select, all possibilities are implemented. The
general structure is equivalent to minecraft:

````kotlin
val command = "/tag ${Selector.a["family=player", "tag=coding"] add test2}"
````

but to make development a bit more streamlined we can also represent the command as follows:

````kotlin
val command = "/tag ${Selector.a[family("player"), tag("coding")] add test2}"
````

*Selector wiki*

Select the n nearest players: `Selector.a[c(value = 2)]`

Select entities on a certain height range (height 2 till 2+5 = 7): `Selector.a[y(2), dy(5)]` 