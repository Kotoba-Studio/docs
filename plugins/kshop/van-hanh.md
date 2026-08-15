---
description: Theo dõi giao dịch và xử lý lỗi KShop phổ biến.
icon: wrench
---

# Vận hành

## Vận hành KShop R04 – HotFix

### Giao dịch

KShop xử lý giao dịch theo queue riêng của từng người chơi.

`purchase.queue-capacity` giới hạn click đang chờ. Giá trị mặc định là `16`.

`purchase.quote-expire-seconds` xác định thời hạn quote. Giá mặc định hết hạn sau `15` giây.

KShop tạo transaction ID và ghi journal. Idempotency chặn callback commit hai lần.

Plugin kiểm tra provider, giá, balance và reward trước commit. Journal trạng thái mơ hồ được giữ lại.

{% hint style="warning" %}
Không xóa journal để ép giao dịch tiếp tục. Đối chiếu audit và economy log trước.
{% endhint %}

### Price Guard

Price Guard ngăn vòng lặp mua, craft rồi bán qua KWorth.

```yaml
price:
  guard:
    enabled: true
    fail-closed: true
    margin-percent: 5.0
    crafting:
      enabled: true
```

Thêm crafting floor cho material cần bảo vệ. Kiểm tra giá với multiplier bán cao nhất.

Khi KWorth không đọc được giá, `fail-closed` chặn giao dịch. Không tắt cơ chế này trên production.

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

### Currency không khả dụng

Kiểm tra `eco:` trên chính product.

```yml
eco: vault
```

`points` cần PlayerPoints. `shards` cần KShards. `vault` cần Vault và economy hoạt động.

### `/shop` không phản hồi hoặc category trống

Kiểm tra `kshop.open` và lỗi load trong console.

Chạy `/kshop status`, rồi kiểm tra category có file tại `styles/<active-style>/shops/<category>.yml`.

Kiểm tra `root.categories` nếu category phải xuất hiện trong root menu.

### Product không load

Kiểm tra material, price, command, YAML indentation, slot và product ID.

### Menu không có tiếng

Kiểm tra `enabled: true` trong `sounds.yml`.

Khi tắt success chat, success sound vẫn có thể phát.

### Rank không được cấp

Kiểm tra `plugins/KShop/ranks/settings.yml` và command của rank item.

Với `provider: custom`, `set-command` và `add-command` không được để trống.

Nếu `/ranks` không mở, bật `rank-shop.enabled: true`, reload và kiểm tra `kshop.ranks.open`.

### Language chưa đổi

Đổi `lang:` rồi chạy `/kshop reload`.

KShop dùng fallback language khi cần.

### Lỗi sau khi nâng cấp

Restart hoàn toàn máy chủ. Không dùng `/reload` của Bukkit.

Giữ thư mục dữ liệu và chỉ thay JAR. Không để nhiều JAR KShop cùng tồn tại.

### Layout bị lỗi

Kiểm tra slot theo size inventory. Menu 27 slot chỉ dùng `0` đến `26`.

Kiểm tra `product-slots`, `category-slots`, navigation và selector không đè nhau.

### Purchase bị từ chối khi không có tiền

Kiểm tra `eco: vault` trên sản phẩm. Xác nhận `/kshop status` nhận đúng money provider.

So sánh số dư với economy plugin. Kiểm tra currency không phải `shards` hoặc `points`.

Thiếu tiền luôn báo riêng người mua. Tin báo gồm số cần, số đang có và số thiếu.

### Bundle chẩn đoán

Khi báo lỗi, gửi KShop version, server version, Java version và output `/kshop status`.

Kèm product YAML, economy plugin, console error và bước tái hiện. Không gửi webhook URL hoặc thông tin nhạy cảm.
