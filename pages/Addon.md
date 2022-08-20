# Creating an Addon

## Basics

Within the `Main.kt` is already an addon structure given and hints on what is possible.

````kotlin
addon(
    projectName = "TranClate Adventure",
    projectShort = "ta",
    description = "A adventure of discovering TranClate as great development tool",
    packIcon = getResource("general/pack.png"),
    world = getResource("world/template-world").modifyTemplateWorldName("Template"),
    version = arrayListOf(1, 0, 0)
) {
    packageAddon = false
}
````

Within the header of the addon function we can define some basics of the addon we want to have. The projectShort is
thereby also used as the namespace of entities etc.

Within the Body or the Addon Context we can define entities, items, etc. that will automatically be associated with the
addon. 

## &#128195; Modifications

## &#128296; Build the addon

## &#129514; Experimental Features