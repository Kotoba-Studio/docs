---
description: Tích hợp KOrder trong plugin Java khác.
icon: brackets-curly
---

# Java API

## Java API

<a href="java-api.md" class="button primary">Tiếng Việt</a> <a href="english/java-api.md" class="button secondary">English</a>

Public API package:

```
studio.kotoba.korder.api
```

### Thiết lập

```kotlin
dependencies {
    compileOnly(files("libs/KOrder-R01.jar"))
}
```

Thêm soft dependency vào `plugin.yml`:

```yaml
softdepend: [KOrder]
```

### Kiểm tra KOrder

```java
import studio.kotoba.korder.api.KOrderAPI;

if (!KOrderAPI.isAvailable()) return;
String version = KOrderAPI.version();
```

### Query

```java
KOrderAPI.findOrder(id);
KOrderAPI.ordersByBuyer(uuid, 50);
KOrderAPI.activeOrdersByBuyer(uuid, 50);
KOrderAPI.searchOrders("diamond", 25);
KOrderAPI.activeOrderCount(uuid);
```

Mọi query trả về `CompletableFuture`.

### Mở GUI

```java
KOrderAPI.openOrders(player);
KOrderAPI.openMyOrders(player);
KOrderAPI.openStash(player);
KOrderAPI.openCreate(player);
```

### OrderSnapshot

Các field chính:

```java
order.id();
order.buyerId();
order.buyerName();
order.item();
order.requested();
order.fulfilled();
order.remaining();
order.unitPriceCents();
order.escrowCents();
order.state();
order.active();
order.createdAtMillis();
order.expiresAtMillis();
```

State hợp lệ:

```
ACTIVE
COMPLETED
CANCELLED
EXPIRED
```

{% hint style="warning" %}
Chỉ dùng package `studio.kotoba.korder.api`. Không truy cập trực tiếp `data/korder.db`.

Không thao tác Bukkit Entity trực tiếp trong callback query async trên Folia hoặc Canvas.

R01 không public mutation API cho create, cancel, deliver hoặc payout. Điều này ngăn bypass anti-dupe và escrow.
{% endhint %}
