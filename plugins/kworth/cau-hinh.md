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

Mặc định, giá không giảm dưới giá gốc.

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

### Discord Webhook

```yaml
webhooks:
  discord:
    enabled: false
    url: ''
```

Bật `enabled` và thêm webhook URL để nhận log bán hàng.
