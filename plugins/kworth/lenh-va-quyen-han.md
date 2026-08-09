---
description: Lệnh cho người chơi, quản trị viên và permission nodes.
icon: terminal
---

# Lệnh và quyền hạn

## Lệnh và quyền hạn

| Lệnh                                    | Chức năng                           | Permission              |
| --------------------------------------- | ----------------------------------- | ----------------------- |
| `/sell`                                 | Mở Sell GUI                         | `kworth.sell`           |
| `/sell hand`                            | Bán vật phẩm trên tay               | `kworth.sell.hand`      |
| `/sell all`                             | Bán vật phẩm hợp lệ trong inventory | `kworth.sell.all`       |
| `/worth`                                | Xem giá vật phẩm                    | `kworth.worth`          |
| `/selltool give <player> <tool> [uses]` | Cấp SellTool                        | `kworth.selltool.admin` |
| `/kworth reload`                        | Nạp lại KWorth                      | `kworth.admin`          |

Các giá trị `<tool>` thường dùng: `stick`, `axe`, `wand`.

Dùng `uses: -1` cho SellTool vô hạn khi cấu hình cho phép.
