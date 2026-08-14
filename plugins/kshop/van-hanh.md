---
description: Theo dõi giao dịch và xử lý lỗi KShop phổ biến.
icon: wrench
---

# Vận hành

## Vận hành

### Giao dịch

KShop xử lý giao dịch theo queue riêng của mỗi người chơi.

`purchase.queue-capacity` giới hạn job đang chờ. Thiết lập này giảm spam click và giao dịch trùng.

`purchase.quote-expire-seconds` xác định thời gian quote còn hiệu lực. KShop tính lại giá khi quote hết hạn.

Item product được kiểm tra inventory trước khi trao thưởng. Command product chạy reward command sau bước thanh toán.

Nếu reward thất bại sau khi thanh toán, KShop xử lý refund trên transaction path được hỗ trợ.

### Dynamic Market

Market cần bật đồng thời trong `config.yml` và trên product:

```yaml
market-economy:
  enabled: true
```

```yaml
market: true
```

Giá hiệu lực gần đúng bằng `base price × market multiplier`. Multiplier bắt đầu ở `1.0`, không thấp hơn `1.0` và bị giới hạn bởi `maximum-multiplier`.

Mỗi item đã mua tăng pressure. Pressure giảm theo `recovery-half-life-minutes`.

Reset state:

```
/kshop market reset food.baked_potato
/kshop market reset all
```

State nằm tại `plugins/KShop/data/market.properties`. Không sửa file thủ công.

Webhook Market dùng `webhooks.yml`. Không công khai webhook URL.

### Khắc phục sự cố

### Currency không khả dụng

Kiểm tra `eco:` trên chính item.

```yml
eco: vault
```

`points` cần PlayerPoints. `shards` cần KShards. `vault` cần economy provider phù hợp.

### `/shop` không phản hồi hoặc category trống

Kiểm tra `kshop.open` và lỗi load trong console.

Chạy `/kshop status`, rồi kiểm tra category có file tại `styles/<active-style>/shops/<category>.yml`.

Kiểm tra `root.categories` nếu category phải xuất hiện trong root menu.

### Product không load

Kiểm tra material, price, command, YAML indentation, slot và product ID.

### Menu không có tiếng

Kiểm tra `enabled: true` trong `sounds.yml`. R02-v6 mặc định dùng `minecraft:ui.button.click`.

`confirm.name` có thể để trống. KShop sẽ phát sound kết quả cuối cùng.

### Rank không được cấp

Kiểm tra `plugins/KShop/ranks/settings.yml` và command của rank item.

Với `provider: custom`, `set-command` và `add-command` không được để trống.

Nếu `/ranks` không mở, bật `rank-shop.enabled: true`, reload và kiểm tra `kshop.ranks.open`.

### Language chưa đổi

Đổi `lang:` rồi chạy `/kshop reload`.

KShop dùng fallback language khi cần.

### Lỗi sau khi nâng cấp

Restart hoàn toàn máy chủ. Không dùng `/reload` của Bukkit.

### Layout bị lỗi

Kiểm tra slot theo size inventory. Menu 27 slot chỉ dùng `0` đến `26`.

Kiểm tra `product-slots`, `category-slots`, navigation và selector không đè nhau.

### Purchase bị từ chối khi không có tiền

Kiểm tra `eco: vault` trên sản phẩm. Xác nhận `/kshop status` nhận đúng money provider.

So sánh số dư với economy plugin. Kiểm tra currency không phải `shards` hoặc `points`.

### Bundle chẩn đoán

Khi báo lỗi, gửi KShop version, server version, Java version và output `/kshop status`.

Kèm product YAML, economy plugin, console error và bước tái hiện. Không gửi webhook URL hoặc thông tin nhạy cảm.
