# Practice tasks

### Task 1

Modify the baguette flamethrower to also strike the target entity with lightning. Add a config value `strike-with-lightning` which can be `true` or `false` and controls whether the target entity will be struck with lightning.

??? tip "Hint"
    [https://jd.papermc.io/paper/1.21.8/org/bukkit/World.html#strikeLightning(org.bukkit.Location)](https://jd.papermc.io/paper/1.21.8/org/bukkit/World.html#strikeLightning(org.bukkit.Location))

### Task 2

Create two versions of the baguette flamethrower: One that strikes the target with lightning ('Zeus Baguette Flamethrower'), and one that doesn't (the normal 'Baguette Flamethrower').

### Task 3

Create a Baguette of Supreme Wisdom which allows you to store up to 1000 XP, keeping the normal Baguette of Wisdom too.

### Task 4

Add a 'efficiency' config value to the Baguette of Wisdom. If this is set to, for example, 0.8, then you should only get 80% of your XP back when you discharge the baguette. Remember to add it to lore and create a placeholder!

### Task 5

Create a new item, the Baguette of Divine Judgement. 

This should store XP in the same way that the Baguette of Wisdom does, except when you shift right click, instead of discharging, it should use stored XP to strike lightning at the block you're looking at. Make the amount of required XP configurable and display it in the lore.

### Task 6

Create a new item, the Baguette of Loyalty. When shift right clicked, this item should bind itself to the player to right clicked it. It should then remember to who it is bound. If anyone else tries to bind it after it has been initially bound, they should be smitten with lightning. 

When right clicked, the baguette should heal the person who used it only if they are the person who the baguette is bound to.

The amount which it heals should be configurable. The amount it heals and the name of the bound player should be displayed in the lore.

(This is a slightly harder task than all the other ones, and there are multiple ways to accomplish it)

??? tip "Hint"
    You can't store players directly in PDCs, but you can store a player's UUID.
