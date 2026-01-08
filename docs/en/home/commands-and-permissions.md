# Commands & permissions

## Default commands
| Command                            | Permission                               | Description |
|------------------------------------|------------------------------------------|-------------|
| `/py`                              | `pylon.command.guide`                    | Opens the Pylon guide
| `/py guide`                        | `pylon.command.guide`                    | Gives you the Pylon guide

## Admin commands
| Command                                          | Permission                               | Description |
|--------------------------------------------------|------------------------------------------|-------------|
| `/py confetti <amount> [speed] [lifetime]`       | `pylon.command.confetti`                 | Spawns confetti particles
| `/py debug`                                      | `pylon.command.debug`                    | Gives you the debug item, which can be used to view Pylon block/entity data and forcibly remove Pylon blocks/entities
| `/py exposerecipeconfig <addon> <recipe_type>`   | `pylon.command.exposerecipeconfig`       | Allows recipes to be edited for a specific recipe stype. Doing this will prevent any recipes of the given type from being automatically updated, so use with caution!
| `/py give <player> <item> [amount]`              | `pylon.command.give`                     | Gives a player a Pylon item
| `/py key`                                        | `pylon.command.key`                      | Shows you the key of the Pylon item you're holding in your hand
| `/py research add <player> <research>`           | `pylon.command.research.add`             | Adds the given research to a player
| `/py research addall <player>`                   | `pylon.command.research.addall`          | Adds all researches to a player
| `/py research remove <player> <research>`        | `pylon.command.research.remove`          | Removes the given research from a player
| `/py research points add <player> <amount>`      | `pylon.command.research.points.add`      | Adds research points to a player
| `/py research points get <player>`               | `pylon.command.research.points.get`      | Shows you the number of research points a player has
| `/py research points set <player> <amount>`      | `pylon.command.research.points.set`      | Sets the number of research points a player has
| `/py research points subtract <player> <amount>` | `pylon.command.research.points.subtract` | Removes research points from a player
| `/py setblock <x> <y> <z> <block>`               | `pylon.command.setblock`                 | Sets the given Pylon block at the coordinates provided

## Other permissions
| Permission                     | Description |
|--------------------------------|-------------|
| `pylon.guide.cheat`            | Allows you to use drop, ctrl+drop, or middle click to cheat in items from the Pylon guide |
| `pylon.guide.view_admin_pages` | Allows you to see admin-only guide pages                                                  |
