# Using the language system

## What is a language system?

'Language system' might sound intimidating if you've never used one before, but it's very straightforward. A language system is just a way to make things translateable.

For example, let's suppose I want to create a wonderful new item designed to thrill server admins the world over: the 'Nuclear Bomb'. I write the item code, and then, in my code, I set the item's name to be 'Nuclear Bomb'.
```java
...
// (some code to create the item)
...
item.setName("Nuclear Bomb")
...
```
<small>(not real code - just for demonstration purposes)</small>

Now, suppose we want Spanish speakers to be able to play our addon. Well, in Spanish, that's called 'Bomba Nuclear' according to google translate. But I've hardcoded in 'Nuclear Bomb'... so how can we make sure that Spanish people see 'Bomba Nuclear' instead?

The solution to this is to just use a generic 'translation key'.
```java
...
// (some code to create the item)
...
item.setName("item.nuclear-bomb.name")
...
```
<small>(not real code - just for demonstration purposes)</small>

Now, we can create a different file for each language, containing all the translation keys for that language!
```yaml title="en.yml"
item.nuclear-bomb.name: "Nuclear Bomb"
```
<small>(not real code - just for demonstration purposes)</small>

```yaml title="es.yml"
item.nuclear-bomb.name: "Bomba Nuclear"
```
<small>(not real code - just for demonstration purposes)</small>

Obviously, we'll need some system to substitute in the right translation for the right people, but Pylon will handle that for you automatically. Now, let's see how to do the same thing with Pylon.

---

## Using Pylon's language system

Remember how we did `item.setName("item.nuclear-bomb.name")` above? In Pylon, you don't need to do that because Pylon **automatically generates the translation key** based on your item's key. All we need to do is create translation files and make sure they contain the correct keys.

Let's do this for the Baguette (fom the previous section). Open the 'en.yml' file ('en' is a code for 'English') in the `src/main/resources/lang` folder.

!!! Note "Adding translations for other languages"
    If we wanted to create a Spanish language file, we would call it 'es.yml' - or 'cs.yml' for Czech, and so on. See [this Wikipedia page](https://minecraft.wiki/w/Language) for a full list of these 2-letter codes.

Next, add this inside the file:
```yaml title="en.yml" hl_lines="3-7"
addon: "<your addon name here>"

item:
  baguette:
    name: "Baguette"
    lore: |-
      <arrow> <dark_red>The <blue>best </red>food
```

Note that we have an `addon` key. This is just the name of your addon.

We've also added `name` and `lore` for the baguette. Notice that we're using `baguette` here because that's the key that identifies the baguette, as we specified in this line:
=== "Java" 
    ```java
    NamespacedKey baguetteKey = new NamespacedKey(this, "baguette");
    ```
=== "Kotlin"
    ```kotlin
    val baguetteKey = NamespacedKey(this, "baguette")
    ```

!!! question "What's all this &lt;arrow&gt; and &lt;red&gt; and &lt;/red&gt; business?"
    We go into this in the [Advanced Lore] chapter.

Start up the server again. Your baguette should now have name and lore!
![Baguette with translations](img/baguette.png)

[Advanced Lore]: ../custom-items/advanced-lore.md
