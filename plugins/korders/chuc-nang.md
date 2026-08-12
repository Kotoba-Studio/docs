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

Người bán có thể giao một phần hoặc toàn bộ số lượng còn thiếu. Delivery GUI chỉ là phần xem trước.

KOrder chỉ lấy item thật sau **Confirm**. Khi đó, hệ thống re-check order và inventory dưới transaction guard.

### Quản lý đơn

Đơn đang hoạt động cho phép:

* **Thêm số lượng** — giữ nguyên giá mỗi món và bổ sung escrow.
* **Hủy đơn** — chỉ áp dụng với đơn `ACTIVE` chưa hết hạn.
* Đơn hoàn tất biến mất khỏi **My Orders** ngay.

### Stash

Hàng đã giao được lưu trong Stash bền vững. Nếu inventory không đủ chỗ, phần chưa nhận vẫn được giữ lại.

Khi claim, KOrder đánh dấu entry là `CLAIMING` trước khi lưu player. Điều này ưu tiên chống nhân bản sau crash.

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

`custom.yml` giữ text riêng khi đổi locale. Slot control phải nằm trong `0..53` và không được trùng.

`page-size` được giới hạn trong `9..45`. Stash luôn hiển thị 45 entry mỗi trang.

### Tìm kiếm và input

KOrder ưu tiên native Paper Dialog. Bedrock dùng Floodgate/Geyser form khi khả dụng.

Các client không hỗ trợ Dialog dùng virtual Anvil khi được bật. R02-v2 không đặt sign tạm trong world.

### Tích hợp

* PlaceholderAPI và Discord Webhook.
* Vault, VaultUnlocked v2 và PlayerPoints.
* CoinsEngine và ExcellentEconomy qua Vault provider.
* Geyser và Floodgate khi khả dụng.
