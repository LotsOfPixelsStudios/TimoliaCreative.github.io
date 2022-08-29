# Writing you're own plugin

## Concept

TranClate is built for 2 sides exploits the features of Kotlin 

 - the Minecraft developer, the goal is to keep it simple and familiar to the classic style of writing addons
 - the Plugin developer who wants to access and modify files before, while and after the user can modify them

TranClate tries to introduce concepts fot the Plugin developer to dig deeper into TranClate to access 
parts of the addon, the normal Minecraft developer should not see for complexity reasons.

## Exploiting Extension-functions

If we want to write an accessible plugin for a developer we may want to use an extension-function 
on the `SystemAddon` class. With that we can simply implement within the addon brackets
the additional functions of the plugin.

````kotlin
fun SystemAddon.plane(data: Plane.() -> Unit) {
    val plane = Plane().apply(data)
    //stuff
}

addon {
    plane {
        //define stuff within the Car class
    }
}
````

## Unsafe (experimental &#129514;) 

Most TranClate Objects have an inner class called `Unsafe`. This class contains
data the Minecraft Developer sets and modifies with functions. For plugins, we may want
to access or remove data from these maps - to do that we can go into the unsafe context like:

````kotlin
behEntity {
    unsafe {
        if(general.conatinsKey("test")) {
            //do stuff
        }
    }
}
````

the unsafe object is also accessible as a value within the objects:

````kotlin
behEntity {
    val test = unsafe.general.containsKey("test")
}
````