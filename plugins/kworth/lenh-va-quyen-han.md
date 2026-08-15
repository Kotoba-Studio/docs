---
description: Lệnh cho người chơi, quản trị viên và permission nodes.
icon: terminal
---

# Lệnh và quyền hạn

## Lệnh và quyền hạn

| Lệnh                                    | Chức năng                           | Permission             |
| --------------------------------------- | ----------------------------------- | ---------------------- |
| `/sell`                                 | Mở Sell GUI                         | `kworth.sell`          |
| `/sell hand`                            | Bán vật phẩm trên tay               | `kworth.sell.hand`     |
| `/sell all`                             | Bán vật phẩm hợp lệ trong inventory | `kworth.sell.all`      |
| `/sell price [material]`                | Xem giá vật phẩm                    | `kworth.sell.price`    |
| `/worth [material]`                     | Xem giá vật phẩm                    | `kworth.sell.price`    |
| `/selltool give <player> <tool> [uses]` | Cấp SellTool                        | `kworth.selltool.give` |
| `/kworth reload` hoặc `/sell reload`    | Nạp lại KWorth                      | `kworth.reload`        |
| `/kworth status`                        | Kiểm tra provider và tích hợp       | `kworth.status`        |

`uses: -1` là vô hạn. Chạy `/kworth status` trước khi cấp tool custom.

Tool cần quyền `kworth.selltool.use.<id>`. Legacy config vẫn dùng `stick`, `axe` và `wand`.
