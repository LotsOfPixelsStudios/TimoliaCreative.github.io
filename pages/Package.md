# Package Projects

## &#127757; McWorld/ McAddon

For non Marketplace Projects a McWorld File is the way to go to package and distribute
the project.

TranClate will give a simple option to package the addon:

````kotlin
addon() {

}

zipWorld()
````

To zip just the addon use

````kotlin
addon() {

}

zipAddon()
````

## &#128230; Marketplace Package

To add a simple but correct package execute within the addon the following functions:

````kotlin
addon() {
    packaging {
        packageName = "name of the zip"
        this.world = getResource("world/worldName")
        addSkinPack(validate = true, getResource("skin_pack"))
        addStoreArt { }
        addMarketing { }
        addBehaviorPack { }
        addResourcePack { }
    }
}
````

You can also be a bit more customisable, specify directories etc., for example:

````kotlin
addBehaviorPack {
    packName = "the name of only the beh pack"
    packDescription = "my custom description that modifies only the beh pack"
}
addResourcePack {
    packName = "this name is for the resource pack only"
    packDescription = "custom description"
}
addStoreArt {
    dir = getResource("package/Store-Art")
}
addMarketing {
    dir = getResource("package/Marketing-Art")
}
````

## &#127760; Package with the ci pipeline

In the root level of the project is a `.gitlab-ci.yml` file that will be executed in the gitlab repository when pushed.
We can use this to build the packages and create a release to easily download the artifacts.

We can achieve that like in the template by executing the build command with different args.
We do that to avoid packaging on the local machine of a developer to reduce build time.

The build command in the `.gitlab-ci.yml` looks like:

````yaml
  script:
    - ./gradlew run --args="zip-world package"
````

And the counterpart in the main that is executed:

````kotlin
fun main(args: Array<String>) {
    val zipWorld = args.contains("zip-world")
    val packageAddon = args.contains("package")
}
````

From this we can just build the packages when these booleans are true:

````kotlin
fun main(args: Array<String>) {
    addon() {
        if (args.contains("package")) {
            packageAddonCustom {
                //...
            }
        }
    }
    if (args.contains("zip-world"))
        zipWorld(/* .. */)
}
````