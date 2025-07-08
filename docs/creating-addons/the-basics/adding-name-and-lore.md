# Using the language system

## What is the language system?

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

Now, suppose we want Spanish speakers to be able to play our addon. Well, in Spanish, that's called 'Bomba Nuclear'. But I've hardcoded in 'Nuclear Bomb'... so how can we make sure that Spanish people see 'Bomba Nuclear' instead?

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
```yml title="en.yml"
item.nuclear-bomb.name: "Nuclear Bomb"
```
<small>(not real code - just for demonstration purposes)</small>

```yml title="es.yml"
item.nuclear-bomb.name: "Bomba Nuclear"
```
<small>(not real code - just for demonstration purposes)</small>

Obviously, we'll need some system to substitute in the right translation for the right people, but Pylon will handle that for you, so don't worry about it for now. Now, let's see how to do the same thing with Pylon.

---

## Adding name and lore to our epic sword

Remember how we did `item.setName("item.nuclear-bomb.name")` above? In Pylon, you don't need to do that because Pylon automatically generates the translation key based on your item's key. All we need to do is create translation files and make sure they contain the correct keys.

Create a 'resources' folder under 'main', and then a 'lang' folder under that, and finally an 'en.yml' file (for English). 

![Creating the language file](/img/creating-the-language-file.png)

<details>
    <summary>Adding translations for other languages</summary>
    If we wanted to create a Spanish language file, we would call it 'es.yml' - or 'cs.yml' for Czech, and so on. <a href="https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes">See this Wikipedia page for a full list of these 2-letter codes.</a>
</details>

Next, add this inside the file:
```yml title="en.yml"
addon: "<your addon name here>"

item:
  epic_sword:
    name: "Epic Sword"
    lore: |-
      <arrow> This is an <red>epic</red> sword
      <arrow> Very epic
```

Note that we have an `addon` key. This is just the name of your addon.

We've also added `name` and `lore` for our sword. Notice that we're using `epic_sword` here because that's the key that we created earlier:
```java
NamespacedKey epicSwordKey = new NamespacedKey(this, "epic_sword");
```

<details>
    <summary>What's all this &lt;arrow&gt; and &lt;red&gt; and &lt;/red&gt; business?&lt;summary&gt;</summary>
    We'll go into this more later, but Pylon uses <a href="https://docs.advntr.dev/minimessage/index.html">MiniMessage</a> formatting. Pylon also has its own custom tags - &lt;arrow&gt; is an example of this. (TODO add links to language page)
</details>

Start up the server again. Your sword should now have name and lore!
![Epic sword with translations](/img/epic-sword.png)

