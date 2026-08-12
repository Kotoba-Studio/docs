---
description: Ngôn ngữ, giao diện, economy, webhook và order settings.
icon: gear
---

# Cấu hình

## Cấu hình

<a href="cau-hinh.md" class="button primary">Tiếng Việt</a> <a href="english/configuration.md" class="button secondary">English</a>

File cấu hình chính: `plugins/KOrder/config.yml`.

### Ngôn ngữ

```yaml
language: vi_VN
```

Ngôn ngữ có sẵn: `vi_VN`, `en_US`, `es_ES`, `pt_BR` và `de_DE`.

### Giao diện

```yaml
gui:
  style: modern
```

Các style: `modern`, `king`, `custom`.

`custom` tắt text theo locale. Title custom hỗ trợ `{page}`, `{pages}` và `{order}`.

```yaml
layout:
  page-size: 45

behavior:
  direct-deliver: true
```

### Economy

```yaml
economy:
  bridge: auto
```

| Mode               | Mô tả                                |
| ------------------ | ------------------------------------ |
| `auto`             | VaultUnlocked → Vault → PlayerPoints |
| `vaultunlocked`    | Chỉ VaultUnlocked v2                 |
| `vault`            | Economy provider đăng ký qua Vault   |
| `playerpoints`     | PlayerPoints trực tiếp               |
| `coinsengine`      | CoinsEngine qua Vault provider       |
| `excellenteconomy` | ExcellentEconomy qua Vault provider  |

`vault` chấp nhận mọi Vault Economy provider được đăng ký đúng. CoinsEngine và ExcellentEconomy không có custom-currency ID trực tiếp.

PlayerPoints dùng point nguyên. Giá không biểu diễn chính xác sẽ bị từ chối, không làm tròn.

{% hint style="warning" %}
Không retry mù một deposit hoặc withdraw không chắc chắn. Kiểm tra `/korder admin pending`, `/korder admin tx <id>` và lịch sử economy trước khi bù trừ.
{% endhint %}

### Discord Webhook

```yaml
discord-webhook:
  enabled: false
  url: ''
  username: KOrder
  events:
    - order-created
    - order-increased
    - order-delivered
    - order-completed
    - order-cancelled
    - order-expired
    - transaction-warning
```

Kiểm tra webhook bằng `/korder admin webhook test`.

Webhook chạy ngoài transaction. Hàng đợi có giới hạn 256 message. Lỗi webhook không rollback hoặc nhân bản order.

### Đơn hàng

```yaml
orders:
  default-limit: 3
  expiry-days: 7
  min-amount: 1
  max-amount: 2304
  allow-own-delivery: false
  exact-item-from-hand: true
```
