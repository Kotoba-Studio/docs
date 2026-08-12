---
description: Lệnh cho người chơi, quản trị viên và permission nodes.
icon: terminal
---

# Lệnh và quyền hạn

## Lệnh và quyền hạn

<a href="lenh-va-quyen-han.md" class="button primary">Tiếng Việt</a> <a href="english/commands-and-permissions.md" class="button secondary">English</a>

KOrder dùng `/korder` với các alias `/order`, `/orders` và `/donhang`.

### Người chơi

| Lệnh                                         | Quyền            | Chức năng                      |
| -------------------------------------------- | ---------------- | ------------------------------ |
| `/korder`                                    | `korder.use`     | Mở chợ                         |
| `/korder help`                               | —                | Xem trợ giúp theo locale       |
| `/korder browse [từ khóa]`                   | `korder.use`     | Xem đơn công khai              |
| `/korder public [từ khóa]`                   | `korder.use`     | Alias của `browse`             |
| `/korder search <từ khóa>`                   | `korder.use`     | Gợi ý buyer và tìm order       |
| `/korder create`                             | `korder.create`  | Mở tạo đơn                     |
| `/korder create <material> <số lượng> <giá>` | `korder.create`  | Tạo đơn bằng Material          |
| `/korder createhand`                         | `korder.create`  | Tạo đơn từ item đang cầm       |
| `/korder mine` / `my`                        | `korder.use`     | Xem đơn `ACTIVE`, chưa hết hạn |
| `/korder stash` / `collect`                  | `korder.use`     | Mở Stash                       |
| `/korder deliver <id> <số lượng>` / `giao`   | `korder.deliver` | Giao item                      |
| `/korder add <id> <số lượng>`                | `korder.create`  | Tăng số lượng đơn              |

`increase` và `them` là alias của `add`.

### Quản trị

| Lệnh                         | Quyền          | Chức năng                                     |
| ---------------------------- | -------------- | --------------------------------------------- |
| `/korder reload`             | `korder.admin` | Tải lại config, style, economy và integration |
| `/korder admin info`         | `korder.admin` | Xem trạng thái plugin                         |
| `/korder admin pending`      | `korder.admin` | Xem transaction cần kiểm tra                  |
| `/korder admin tx <id>`      | `korder.admin` | Xem một transaction                           |
| `/korder admin webhook test` | `korder.admin` | Kiểm tra Discord Webhook                      |
| `/korder admin`              | `korder.admin` | Xem trợ giúp quản trị                         |
| `/korder admin reload`       | `korder.admin` | Alias của `/korder reload`                    |

### Permission nodes

```
korder.use
korder.create
korder.deliver
korder.admin
korder.update.notify
korder.bypass.creative
```

#### Giới hạn số đơn

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

Nếu người chơi có nhiều quyền giới hạn, KOrder dùng giá trị cao nhất thay cho `orders.default-limit`.
