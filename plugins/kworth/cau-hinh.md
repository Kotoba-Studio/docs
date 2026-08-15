---
description: Giao diện, xác nhận bán, giá thị trường, economy và webhook.
icon: gear
---

# Cấu hình

## Cấu hình

KWorth lưu các tệp chính tại:

```
plugins/KWorth/
├─ config.yml
├─ messages.yml
├─ prices.yml
├─ selltool.yml
├─ Settings/
└─ data/
```

### Sell GUI

```yaml
gui:
  style: king
```

Các style có sẵn: `king`, `simple`, `modern`, `compact`, `midnight`, `custom`.

Tạo tệp `.yml` trong `Settings/` để thêm style. Đặt tên style đó trong `config.yml`.

### Nút xác nhận

```yaml
sell:
  confirm-button: true
```

* `true`: người chơi phải bấm nút xác nhận.
* `false`: đóng GUI sẽ tự bán vật phẩm bên trong.

### Market Price

Market Price có thể bật hoặc tắt trong `config.yml`. Khi bật, giá thay đổi theo lượng vật phẩm đã bán.

`floor-at-base` ngăn giá hiệu lực thấp hơn base worth sau progression. Kiểm tra `/worth` sau reload.

`prices.yml` dùng Bukkit Material hợp lệ. Giá phải lớn hơn `0`. Giá cuối kết hợp base worth, progression và market.

### Economy

Dùng Vault:

```yaml
economy:
  provider: vault
```

Dùng KShards:

```yaml
economy:
  provider: kshards
  fallback-to-vault: false
```

Provider hỗ trợ: `vault`, `vaultunlocked`, `excellenteconomy`, `coinsengine`, `kshards`. `currency-id` dùng cho ExcellentEconomy.

Chỉ fallback sang Vault trước transaction khi provider chưa sẵn sàng. Không fallback sau lỗi mơ hồ.

Với KShards, chọn rõ `multiplier` và `rounding`: `nearest`, `floor` hoặc `ceil`.

### Discord Webhook

```yaml
webhooks:
  discord:
    enabled: false
    url: ''
```

Bật `enabled` và thêm webhook URL để nhận log bán hàng.

### Recovery và virtual lore

Giữ `anti-dupe.fail-closed-recovery: true`. Entry mơ hồ tại `data/transaction-journal.yml` phải được đối chiếu transaction ID, log economy và history trước khi bồi hoàn thủ công.

`item-price-display` tắt mặc định và cần PacketEvents. Lore chỉ gửi cho client. Giữ scope mặc định ở player inventory để tránh xung đột GUI.
