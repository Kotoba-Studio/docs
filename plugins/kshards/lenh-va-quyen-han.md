---
description: Lệnh người chơi, quản trị viên và permission nodes.
icon: terminal
---

# Lệnh và quyền hạn

## Lệnh và quyền KShards

### Người chơi

| Lệnh                            | Quyền             |
| ------------------------------- | ----------------- |
| `/shards`                       | `kshards.balance` |
| `/shards balance [player]`      | `kshards.balance` |
| `/shards pay <player> <amount>` | `kshards.pay`     |
| `/shards top [page]`            | `kshards.top`     |
| `/shards history [page]`        | `kshards.history` |
| `/shardshop`                    | `kshards.shop`    |

### Quản trị

| Lệnh                             | Quyền                   |
| -------------------------------- | ----------------------- |
| `/shards give <player> <amount>` | `kshards.admin.give`    |
| `/shards take <player> <amount>` | `kshards.admin.take`    |
| `/shards set <player> <amount>`  | `kshards.admin.set`     |
| `/shards reset <player>`         | `kshards.admin.reset`   |
| `/shards freeze <player>`        | `kshards.admin.freeze`  |
| `/shards inspect <player>`       | `kshards.admin.inspect` |
| `/shards reload`                 | `kshards.admin.reload`  |
| `/shards status`                 | `kshards.admin.status`  |

Quyền quản trị tổng: `kshards.admin`.
