# Creating an Addon

## Basics

Within the `Main.kt` is already an addon structure given and hints on what is possible.

````kotlin
addon({
    projectName = "TranClate Adventure"
    projectShort = "ta"
    description = "A adventure of discovering TranClate as great development tool"
    packIcon = getResource("general/pack.png")
    world = getResource("world/template-world").modifyTemplateWorldName("Template")
    version = arrayListOf(0, 0, 1)
}) {

}
````

Within the header of the addon function we can define some basics of the addon we want to have. The projectShort is
thereby also used as the namespace of entities etc.

Within the Body or the Addon Context we can define entities, items, etc. that will automatically be associated with the
addon.

## &#128195; Modifications

This section may be interesting for publishing the addon, as for example overwriting the end users version may be
a bit different as on the machine of the developer:

### version

The version of the addon defaults to `0.0.1`, if you decide to release a new version of the addon consider
bumping the version with the following principal: `<major>.<minor>.<patch>`. So bump the first number when releasing
or a braking change has happened. The second number when a new feature/enhancement is released and third when a small
fix
has taken place.

### Target Mc Version

Modify the target Mc Version if you want to indicate that the addon was build in a older version of Minecraft.
Note: You may not use components of a newer Version then.

Access the target mc version:

```kotlin
addon(/*...*/) {
    properties.targetMcVersion = arrayListOf(1, 19, 30)
}
```

### My mc folder can't be found

This can happen if minecraft wasn't installed with the default parameters, change the direcotry like:

```kotlin
addon(/*...*/) {
    properties.comMojangPath =
        System.getenv("LOCALAPPDATA") + "\\Packages\\Microsoft.MinecraftUWP_8wekyb3d8bbwe\\LocalState\\games\\com.mojang"
}
```

## &#128296; Build the addon

### Local Build

As a default, the whole addon will be pushed to the minecraft folder after executing. TranClate will ensure that old
files
will be deleted with some limitations:

- can't delete if the projectName/projectShort has changed
- minecraft is running with the world open (this will produce an exception)

If you don't want to push the addon the minecraft folder, disable it by

````kotlin
addon(/*...*/) {
    buildToMcFolder = false
}
````

you can also disable other things like:

````kotlin
buildFunctions = false
buildTextureList = false
buildItemTextureIndex = false
buildToMcFolder = false
````

### Pipeline Build

The template has for both GitHub (Actions) and GitLab pipeline templates that can be modified to build and package the
addon.

Default is to add a Tag (GitLab) or Release (GitHub) to trigger the pipeline to add the package to the release/tag.

To correctly package the addon, see the Package page.

## &#129514; Experimental Features

Currently, Blockbench Files are experimental, more in the Entity documentation.