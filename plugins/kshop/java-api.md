---
description: Mở Shop GUI từ plugin Java khác.
icon: brackets-curly
---

# Java API

## KShop API

Khai báo KShop là dependency tùy chọn:

```yaml
softdepend: [KShop]
```

### Mở GUI

```java
import vn.kotobastudio.kshopr01.KShopR01;

KShopR01 shop = KShopR01.instance();
shop.openShop(player);
shop.openShop(player, "shards");
shop.openRanks(player);
```

{% hint style="warning" %}
Khi dùng `softdepend`, luôn kiểm tra KShop đã được bật trước khi gọi API.
{% endhint %}
