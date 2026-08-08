---
description: Buy Order, giao hàng, Stash và tích hợp.
icon: sparkles
---

# Chức năng

## Chức năng

<a href="chuc-nang.md" class="button primary">Tiếng Việt</a> <a href="english/features.md" class="button secondary">English</a>

### Buy Order

Người mua chọn vật phẩm, số lượng và giá mỗi món. KOrder xác thực dữ liệu trước khi đưa tổng tiền vào escrow.

### Giao hàng

Người bán có thể giao một phần hoặc toàn bộ số lượng còn thiếu. GUI chỉ chọn số lượng. Item thật chỉ bị lấy khi chọn **Confirm** và transaction được kiểm tra lại.

### Quản lý đơn

Đơn đang hoạt động cho phép:

* **Thêm số lượng** — giữ nguyên giá mỗi món và bổ sung escrow.
* **Hủy đơn** — chỉ áp dụng với đơn `ACTIVE` chưa hết hạn.
* Đơn hoàn tất biến mất khỏi **My Orders** ngay.

### Stash

Hàng đã giao được lưu trong Stash. Nếu inventory không đủ chỗ, phần chưa nhận vẫn được giữ lại.

### Giao diện

```
modern  — mặc định, gọn và hiện đại
king    — bố cục KingMC/Donut-style
custom  — tùy chỉnh text và layout riêng
```

Các preset nằm trong `plugins/KOrder/settings/`:

```
modern.yml
king.yml
custom.yml
```

### Tích hợp

* PlaceholderAPI và Discord Webhook.
* Vault, VaultUnlocked và PlayerPoints.
* CoinsEngine, ExcellentEconomy, Geyser và Floodgate khi khả dụng.
