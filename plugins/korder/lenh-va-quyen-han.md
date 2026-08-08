---
description: Lệnh cho người chơi, quản trị viên và permission nodes.
icon: terminal
---

# Lệnh và quyền hạn

## Lệnh và quyền hạn

<a href="lenh-va-quyen-han.md" class="button primary">Tiếng Việt</a> <a href="english/commands-and-permissions.md" class="button secondary">English</a>

KOrder dùng `/korder` với các alias `/order`, `/orders` và `/donhang`.

### Người chơi

| Lệnh                                        | Quyền            | Chức năng                |
| ------------------------------------------- | ---------------- | ------------------------ |
| `/order`                                    | `korder.use`     | Mở chợ Order             |
| `/order help`                               | —                | Xem trợ giúp             |
| `/order browse [từ khóa]`                   | `korder.use`     | Xem đơn công khai        |
| `/order search <từ khóa>`                   | `korder.use`     | Tìm đơn                  |
| `/order create`                             | `korder.create`  | Mở tạo đơn               |
| `/order create <material> <số lượng> <giá>` | `korder.create`  | Tạo đơn bằng Material    |
| `/order createhand`                         | `korder.create`  | Tạo đơn từ item đang cầm |
| `/order mine`                               | `korder.use`     | Xem My Orders            |
| `/order stash`                              | `korder.use`     | Nhận hàng                |
| `/order deliver <id> <số lượng>`            | `korder.deliver` | Giao hàng                |
| `/order add <id> <số lượng>`                | `korder.create`  | Thêm số lượng vào đơn    |

Alias có sẵn: `public`, `my`, `collect`, `giao`, `increase`, `them`.

### Quản trị

| Lệnh                         | Quyền          | Chức năng                                     |
| ---------------------------- | -------------- | --------------------------------------------- |
| `/korder reload`             | `korder.admin` | Tải lại config, style, economy và integration |
| `/korder admin info`         | `korder.admin` | Xem trạng thái plugin                         |
| `/korder admin pending`      | `korder.admin` | Xem transaction cần kiểm tra                  |
| `/korder admin tx <id>`      | `korder.admin` | Xem một transaction                           |
| `/korder admin webhook test` | `korder.admin` | Kiểm tra Discord Webhook                      |

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

Nếu người chơi có nhiều quyền giới hạn, KOrder dùng giá trị cao nhất.
