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
    compileOnly(files("libs/KOrder-R02-v2.jar"))
}
```

Thêm soft dependency vào `plugin.yml`:

```yaml
softdepend: [KOrder]
```

Chỉ dùng `depend: [KOrder]` khi plugin không thể hoạt động nếu thiếu KOrder.

### Kiểm tra KOrder

```java
import studio.kotoba.korder.api.KOrderAPI;

if (!KOrderAPI.isAvailable()) return;
String version = KOrderAPI.version(); // R02-v2
```

### Query

```java
KOrderAPI.findOrder(id);
KOrderAPI.ordersByBuyer(uuid, 50);
KOrderAPI.activeOrdersByBuyer(uuid, 50);
KOrderAPI.searchOrders("diamond", 25);
KOrderAPI.suggestActiveBuyers("v3", 20);
KOrderAPI.activeOrderCount(uuid);
```

Mọi query trả về `CompletableFuture`. Ngoại trừ `isAvailable()`, mọi API có thể ném `IllegalStateException` nếu KOrder chưa sẵn sàng.

`findOrder` trả `CompletableFuture<Optional<OrderSnapshot>>`. Query database/I/O có thể hoàn tất exceptionally.

`ordersByBuyer` trả lịch sử, gồm `ACTIVE`, `COMPLETED`, `CANCELLED` và `EXPIRED`. `activeOrdersByBuyer` chỉ trả `ACTIVE`, chưa hết hạn.

`searchOrders` chỉ trả order công khai `ACTIVE`, chưa hết hạn. `suggestActiveBuyers` khớp username không phân biệt hoa thường. Các query order dùng limit `1..200`; suggest dùng `1..45`.

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

`item()` luôn trả clone. `active()` chỉ là snapshot check, không phải transaction lock.

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

R02-v2 không public mutation API cho create, cancel, deliver hoặc payout. Điều này ngăn bypass anti-dupe và escrow.

Query hoàn tất trên I/O executor của KOrder. Trên Folia hoặc Canvas, hãy reschedule Bukkit entity/world work bằng entity scheduler của plugin bạn.
{% endhint %}
