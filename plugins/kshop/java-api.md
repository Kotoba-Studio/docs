---
description: Mở Shop GUI từ plugin Java khác.
icon: brackets-curly
---

# Java API

## KShop API

Khai báo JAR KShop khi biên dịch:

```gradle
dependencies {
    compileOnly files('libs/KShop-R02-v6.jar')
}
```

Khai báo dependency cho plugin tích hợp:

```yml
depend: [KShop]
```

### Mở GUI

```java
import vn.kotobastudio.kshopr01.KShopR01;

KShopR01 shop = KShopR01.instance();
shop.openShop(player);
shop.openShop(player, "blocks");
shop.openRanks(player);
```

Package vẫn là `vn.kotobastudio.kshopr01` để giữ compatibility với integration cũ.

API public gồm `instance()`, `openShop(Player)`, `openShop(Player, String)` và `openRanks(Player)`.

{% hint style="warning" %}
Config, transaction, market và economy nội bộ không phải stable API. Không bind trực tiếp plugin khác vào chúng.
{% endhint %}
