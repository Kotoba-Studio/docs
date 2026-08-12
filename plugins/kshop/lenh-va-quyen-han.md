---
description: Lệnh người chơi, quản trị viên và permission nodes.
icon: terminal
---

# Lệnh và quyền hạn

## Lệnh và quyền KShop

| Lệnh                                   | Quyền                |
| -------------------------------------- | -------------------- |
| `/shop [category]`                     | `kshop.open`         |
| `/ranks` hoặc `/rankshop`              | `kshop.ranks.open`   |
| `/kshop status`                        | `kshop.admin.status` |
| `/kshop reload`                        | `kshop.admin.reload` |
| `/kshop style <style>`                 | `kshop.admin.style`  |
| `/kshop open <shop>`                   | `kshop.admin.open`   |
| `/kshop price <shop> <item> <price>`   | `kshop.admin.edit`   |
| `/kshop amount <shop> <item> <amount>` | `kshop.admin.edit`   |
| `/kshop eco <shop> <item> <eco>`       | `kshop.admin.edit`   |
| `/kshop market reset [item\|all]`      | `kshop.admin.market` |

`<eco>` nhận `vault`, `shards`, `points` hoặc `free`.

Quyền `kshop.admin` kế thừa toàn bộ quyền quản trị trong bảng.
