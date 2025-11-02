# Adding a recipe

## Overview

Recipes are stored as YAML files in the `resources/recipes` folder of your addon. For example, in Pylon base, the recipe for tin nuggets is stored in `resources/recipes/minecraft/crafting_shapeless.yml` and looks like this:

```yaml title="crafting_shapeless.yml"
pylonbase:tin_nuggets_from_tin_ingot:
  ingredients:
    - pylonbase:tin_ingot
  result:
    pylonbase:tin_nugget: 9
```

Each recipe type has a specific YAML structure you must follow when writing recipes for it.

!!! info Writing recipe configs
    If you are not sure how to write a config for a specific type of recipe, look for YAML files corresponding to that recipe type. For example, you could look at the [`resources/recipes` folder of Pylon base](https://github.com/pylonmc/pylon-base/tree/master/src/main/resources/recipes/pylonbase) to see how to create a magic altar recipe.

---

## Creating a recipe for the baguette

Dough can be smelted into bread in a normal furnace or smoker. However, for the baguette, we need something more heavy duty: the blast furnace.

Let's create a recipe that smelts dough into baguettes in a blast furnace.

Pylon base already has [an example of how to write blasting recipes](https://github.com/pylonmc/pylon-base/blob/master/src/main/resources/recipes/minecraft/blasting.yml), so let's look there.

Based off of that, let's create our recipe. First, create a file `resources/recipes/minecraft/blasting.yml`. Then, insert the following (and change `myaddon` to the key of your addon):
```yaml
pylonbase:baguette_blasting:
  ingredient: pylonbase:dough
  result: myaddon:baguette
  experience: 0.5
  category: misc
```

The first line is the **key** of the recipe. All recipes of a given type must have a unique key. The rest of the recipe YAML is fairly self explanatory, except perhaps `category`, which is the category that the recipe should appear in in the crafting book.

!!! info Finding item keys
    If you're not sure what an item's key is, hold it in your hand and run `/py key`.

!!! note "From now on, recipes will not be provided for any item examples for the sake of brevity."
