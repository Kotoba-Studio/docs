---
description: Player and administrator commands, plus permission nodes.
icon: terminal
---

# Commands and permissions

## Commands and permissions

<a href="../lenh-va-quyen-han.md" class="button secondary">Tiếng Việt</a> <a href="commands-and-permissions.md" class="button primary">English</a>

KOrder uses `/korder` with `/order`, `/orders`, and `/donhang` aliases.

### Player commands

| Command                                     | Permission       | Description                        |
| ------------------------------------------- | ---------------- | ---------------------------------- |
| `/order`                                    | `korder.use`     | Open the Order marketplace         |
| `/order help`                               | —                | View help                          |
| `/order browse [keyword]`                   | `korder.use`     | View public orders                 |
| `/order search <keyword>`                   | `korder.use`     | Search orders                      |
| `/order create`                             | `korder.create`  | Open order creation                |
| `/order create <material> <amount> <price>` | `korder.create`  | Create an order using a Material   |
| `/order createhand`                         | `korder.create`  | Create an order from the held item |
| `/order mine`                               | `korder.use`     | View My Orders                     |
| `/order stash`                              | `korder.use`     | Collect items                      |
| `/order deliver <id> <amount>`              | `korder.deliver` | Deliver items                      |
| `/order add <id> <amount>`                  | `korder.create`  | Add quantity to an order           |

Available aliases: `public`, `my`, `collect`, `giao`, `increase`, `them`.

### Administrator commands

| Command                      | Permission     | Description                                     |
| ---------------------------- | -------------- | ----------------------------------------------- |
| `/korder reload`             | `korder.admin` | Reload config, style, economy, and integrations |
| `/korder admin info`         | `korder.admin` | View plugin status                              |
| `/korder admin pending`      | `korder.admin` | View transactions requiring review              |
| `/korder admin tx <id>`      | `korder.admin` | View one transaction                            |
| `/korder admin webhook test` | `korder.admin` | Test the Discord Webhook                        |

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

When several limit permissions apply, KOrder uses the highest value.
