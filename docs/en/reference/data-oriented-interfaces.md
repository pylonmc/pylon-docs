# Data-oriented interfaces

`AUTHOR: Idra`
`HAS CONTEXT: Idra, Seggan`

## What the hell is that? I'm scared

Ok 'data-oriented interfaces' sounds really intimidating but I promise it's not. Basically, we much prefer to use interfaces instead of classes because we can inherit from multiple interfaces (well, there are some other reasons too but nevermind that). The problem is of course that interfaces can't have fields.

So traditionally, we might solve that like this. Imagine we have want to store the block's direction, like in `PylonDirectionalBlock`. We might do this:

```kotlin
interface PylonDirectionalBlock {
    val facing
}
```

Now we've forced the block to handle this for us. But think about it. This is really annoying because the block has to now also handle all the loading/unloading logic (it has to write the direction in `write` and then load it again in the load constructor). Which is a lot of extra code if we start doing this for lots of interfaces.

## How do we solve that then?

What we're going to do is just have a map which stores the face of each `PylonDirectionalBlock`, like this:

```kotlin
interface PylonDirectionalBlock {
    var facing: BlockFace
        get() = directionalBlocks[this] ?: error("No direction was set for block $key")
        set(value) {
            directionalBlocks[this] = value
        }
    
    companion object {
        private val directionalBlocks = IdentityHashMap<PylonDirectionalBlock, BlockFace>()
    }
}
```

One other thing, we need to make sure that we store and load the direction at the same time as the block:

```kotlin
@EventHandler
private fun onDeserialize(event: PylonBlockDeserializeEvent) {
    val block = event.pylonBlock
    if (block is PylonDirectionalBlock) {
        directionalBlocks[block] = event.pdc.get(directionalBlockKey, PylonSerializers.BLOCK_FACE)
            ?: error("Direction not found for ${block.key}")
    }
}

@EventHandler
private fun onSerialize(event: PylonBlockSerializeEvent) {
    val block = event.pylonBlock
    if (block is PylonDirectionalBlock) {
        event.pdc.set(directionalBlockKey, PylonSerializers.BLOCK_FACE, directionalBlocks[block]!!)
    }
}
```

That's basically it.
