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

`<eco>` nhận `vault`, `shards`, `kshards`, `points`, `playerpoints` hoặc `free`.

### Mặc định

`kshop.open` và `kshop.ranks.open` mặc định là `true`.

`kshop.admin` và toàn bộ quyền quản trị mặc định dành cho OP. `kshop.admin` kế thừa mọi quyền quản trị trong bảng.

### Product permission

Sản phẩm có thể yêu cầu permission riêng:

```yaml
permission: kshop.vip
```

Người chơi thiếu quyền này không thể mua sản phẩm.

{% hint style="warning" %}
Không cấp `kshop.admin` cho người chơi thường. Quyền này có thể đổi giá, currency và reset Market Economy.
{% endhint %}
