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

`/shards shop` và `/shopshards` cũng mở KShop. Amount nhận `10000`, `10k`, `1.5m` và `2b`.

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

Thêm reason tùy chọn cho `give`, `take`, `set`, `reset`, `freeze` và `unfreeze`. `/shards history <player> [page]` cần `kshards.admin.history`.

### Event và region

* `/shards event x2 4m 4d 4h`, `/shards event status`, `/shards event stop` — `kshards.admin.event`.
* `/kshardsregion set|enable|disable|remove|list|reload` — `kshards.admin.region`.

Event chấp nhận thời lượng ghép. `4m` là bốn phút. State dùng epoch và giữ chính xác qua restart.

`kshards.admin` là parent quản trị. Bypass gồm `kshards.admin.self`, `kshards.admin.high-value`, `kshards.admin.bypass-command-limits`, `kshards.admin.bypass-frozen` và `kshards.admin.bypass-limits`.

Không cấp bypass cho staff không xử lý economy. Giữ `allow-self-modification: false` trừ khi cần thiết.
