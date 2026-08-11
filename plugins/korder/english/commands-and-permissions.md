---
description: Player and administrator commands, plus permission nodes.
icon: terminal
---

# Commands and permissions

## Commands and permissions

<a href="../lenh-va-quyen-han.md" class="button secondary">Tiếng Việt</a> <a href="commands-and-permissions.md" class="button primary">English</a>

KOrder uses `/korder` with `/order`, `/orders`, and `/donhang` aliases.

### Player commands

| Command                                      | Permission       | Description                      |
| -------------------------------------------- | ---------------- | -------------------------------- |
| `/korder`                                    | `korder.use`     | Open the marketplace             |
| `/korder help`                               | —                | View localized help              |
| `/korder browse [query]`                     | `korder.use`     | Open public orders               |
| `/korder public [query]`                     | `korder.use`     | `browse` compatibility alias     |
| `/korder search <query>`                     | `korder.use`     | Suggest buyers and search orders |
| `/korder create`                             | `korder.create`  | Open order creation              |
| `/korder create <material> <amount> <price>` | `korder.create`  | Create using a Material          |
| `/korder createhand`                         | `korder.create`  | Create from the held item        |
| `/korder mine` / `my`                        | `korder.use`     | View active, unexpired orders    |
| `/korder stash` / `collect`                  | `korder.use`     | Open Stash                       |
| `/korder deliver <id> <amount>` / `giao`     | `korder.deliver` | Deliver items                    |
| `/korder add <id> <amount>`                  | `korder.create`  | Increase an order                |

`increase` and `them` are aliases of `add`.

### Administrator commands

| Command                      | Permission     | Description                                     |
| ---------------------------- | -------------- | ----------------------------------------------- |
| `/korder reload`             | `korder.admin` | Reload config, style, economy, and integrations |
| `/korder admin info`         | `korder.admin` | View plugin status                              |
| `/korder admin pending`      | `korder.admin` | View transactions requiring review              |
| `/korder admin tx <id>`      | `korder.admin` | View one transaction                            |
| `/korder admin webhook test` | `korder.admin` | Test the Discord Webhook                        |
| `/korder admin`              | `korder.admin` | View administrator help                         |
| `/korder admin reload`       | `korder.admin` | Alias of `/korder reload`                       |

### Permission nodes

```
korder.use
korder.create
korder.deliver
korder.admin
korder.update.notify
korder.bypass.creative
```

#### Order limits

```
korder.limit.5
korder.limit.10
korder.limit.15
korder.limit.20
korder.limit.30
korder.limit.50
korder.limit.100
korder.limit.200
```

When several limit permissions apply, KOrder uses the highest value over `orders.default-limit`.
