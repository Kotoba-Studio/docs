---
description: Theo dõi giao dịch và xử lý lỗi KShop phổ biến.
icon: wrench
---

# Vận hành

## Vận hành

### Giao dịch

KShop xử lý giao dịch theo queue riêng của mỗi người chơi.

`purchase.queue-capacity` giới hạn job đang chờ. Thiết lập này giảm spam click và giao dịch trùng.

KShop journal các state `PREPARE`, `PAID`, `COMMIT`, `REFUND`, `REJECT` và `MANUAL_REVIEW`.

{% hint style="warning" %}
Không tự refund mọi transaction chưa `COMMIT` sau crash.

Item hoặc command có thể đã được trao. Các transaction mơ hồ cần được review.
{% endhint %}

`purchase.quote-expire-seconds` xác định thời gian quote còn hiệu lực. KShop tính lại giá khi quote hết hạn.

### Khắc phục sự cố

### Currency không khả dụng

Kiểm tra `eco:` trên chính item.

```yml
eco: vault
```

`points` cần PlayerPoints. `shards` cần KShards. `vault` cần economy provider phù hợp.

### Menu không có tiếng

Kiểm tra `enabled: true` trong `sounds.yml`. R02-v6 mặc định dùng `minecraft:ui.button.click`.

`confirm.name` được để trống. Không đặt success sound tại đây nếu muốn tránh âm thanh chồng nhau.

### Rank không được cấp

Kiểm tra `plugins/KShop/ranks/settings.yml` và command của rank item.

Với `provider: custom`, `set-command` và `add-command` không được để trống.

### Language chưa đổi

Đổi `lang:` rồi chạy `/kshop reload`.

KShop giữ language đang dùng hoặc fallback an toàn khi file remote không hợp lệ.

### Lỗi sau khi nâng cấp

Restart hoàn toàn máy chủ. Không dùng `/reload` của Bukkit.
