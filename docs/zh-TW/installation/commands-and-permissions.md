# 指令與權限

## 預設指令
| 指令(Command)                      | 權限(Permission)                         |
|------------------------------------|------------------------------------------|
| `/py`                              | `pylon.command.guide`                    |
| `/py guide`                        | `pylon.command.guide`                    |
| `/py research discover <research>` | `pylon.command.research.discover`        |
| `/py research list`                | `pylon.command.research.list`            |
| `/py research points me`           | `pylon.command.research.points.get.self` |
| `/py waila`                        | `pylon.command.waila`                    |

## 管理員指令
| 指令(Command)                                    | 權限(Permission)                     |
|--------------------------------------------------|-------------------------------------|
| `/py debug`                                      | `pylon.command.debug`               |
| `/py give <player> <item> [amount]`              | `pylon.command.give`                |
| `/py key`                                        | `pylon.command.key`                 |
| `/py research points get <player>`               | `pylon.command.research.points.get` |
| `/py research add <player> <research>`           | `pylon.command.research.modify`     |
| `/py research addall <player>`                   | `pylon.command.research.modify`     |
| `/py research remove <player> <research>`        | `pylon.command.research.modify`     |
| `/py research points add <player> <amount>`      | `pylon.command.research.points.set` |
| `/py research points set <player> <amount>`      | `pylon.command.research.points.set` |
| `/py research points subtract <player> <amount>` | `pylon.command.research.points.set` |
| `/py setblock <block>`                           | `pylon.command.setblock`            |
| `/py confetti <amount>`                          | `pylon.command.confetti`            |
