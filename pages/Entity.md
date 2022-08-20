# Entities

## Basic

## Behaviour

### Components

### Component Groups

### Events

To add and remove Component Groups we can use events by calling within the entity context:

````kotlin
entity {
    events {
        event("event_name") {
            
        }
    }
}

````

#### Default Events

Following default events are also support:

````kotlin
events {
    defaultBornEvent { }
    defaultSpawnedEvent { }
    defaultTransformedEvent { }
    defaultOnPrimeEvent { }
}
````

## Resource

### Notes:
 - If you want to display the entity within the creative inventory you **must** define a spawn egg