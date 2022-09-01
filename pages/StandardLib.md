# &#128218; Standard Library

## State System

## Player

## Furniture

## Command

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