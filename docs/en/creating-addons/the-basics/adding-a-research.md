# Adding a research

## Overview

Adding a research is even easier than adding a recipe. All of an addon's researches are stored in `resources/researches.yml`. For example, here is the 'improved drilling techniques' research:

```yaml title="researches.yml"
...
improved_drilling_techniques:
  material: iron_pickaxe
  cost: 15
  unlocks:
  - pylonbase:improved_manual_core_drill
  - pylonbase:subsurface_core_chunk
...
```

Each research needs a corresponding language entry:
```yaml title="en.yml"
...
research:
  ...
  improved_drilling_techniques: "<#4f4641>Improved drilling techniques"
  ...
```

---

## Adding a research for the baguette

Let's create a research called 'Baguette Supremacy' that unlocks the baguette.

First, create a file `resources/researches.yml`. Inside the file, paste the following (and change `myaddon` to your addon's key):
```yaml title="researches.yml"
baguette_supremacy:
  material: bread
  cost: 3
  unlocks:
  - myaddon:baguette
```

Next, create a `researches` section in `en.yml` and add an entry for the research as follows:

```yaml title="en.yml"
researches:
  baguette_supremacy: "<#ff0000>BAGUETTE SUPREMACY"
```

!!! question "What's this `<#ff0000>` business?"
    This is [hex color code](https://www.howtogeek.com/761277/what-is-a-hex-code-for-colors/) inside a minimessage tag. You can find out more in the [advanced lore](../custom-items/advanced-lore.md) section.

That's it!

!!! note "From now on, researches will not be provided for any item examples for the sake of brevity."
