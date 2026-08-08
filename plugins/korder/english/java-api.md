---
description: Integrate KOrder with another Java plugin.
icon: brackets-curly
---

# Java API

## Java API

<a href="../java-api.md" class="button secondary">Tiếng Việt</a> <a href="java-api.md" class="button primary">English</a>

Public API package:

```
studio.kotoba.korder.api
```

### Setup

```kotlin
dependencies {
    compileOnly(files("libs/KOrder-R01.jar"))
}
```

Add a soft dependency in `plugin.yml`:

```yaml
softdepend: [KOrder]
```

### Check availability

```java
import studio.kotoba.korder.api.KOrderAPI;

if (!KOrderAPI.isAvailable()) return;
String version = KOrderAPI.version();
```

### Queries

```java
KOrderAPI.findOrder(id);
KOrderAPI.ordersByBuyer(uuid, 50);
KOrderAPI.activeOrdersByBuyer(uuid, 50);
KOrderAPI.searchOrders("diamond", 25);
KOrderAPI.activeOrderCount(uuid);
```

Every query returns a `CompletableFuture`.

### Open GUIs

```java
KOrderAPI.openOrders(player);
KOrderAPI.openMyOrders(player);
KOrderAPI.openStash(player);
KOrderAPI.openCreate(player);
```

### OrderSnapshot

Primary fields:

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

Valid states:

```
ACTIVE
COMPLETED
CANCELLED
EXPIRED
```

{% hint style="warning" %}
Use only `studio.kotoba.korder.api`. Do not access `data/korder.db` directly.

Do not access Bukkit Entities inside asynchronous query callbacks on Folia or Canvas.

R01 provides no public mutation API for create, cancel, deliver, or payout. This prevents anti-dupe and escrow bypasses.
{% endhint %}
