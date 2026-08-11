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
    compileOnly(files("libs/KOrder-R02-v2.jar"))
}
```

Add a soft dependency in `plugin.yml`:

```yaml
softdepend: [KOrder]
```

Use `depend: [KOrder]` only when your plugin cannot operate without KOrder.

### Check availability

```java
import studio.kotoba.korder.api.KOrderAPI;

if (!KOrderAPI.isAvailable()) return;
String version = KOrderAPI.version(); // R02-v2
```

### Queries

```java
KOrderAPI.findOrder(id);
KOrderAPI.ordersByBuyer(uuid, 50);
KOrderAPI.activeOrdersByBuyer(uuid, 50);
KOrderAPI.searchOrders("diamond", 25);
KOrderAPI.suggestActiveBuyers("v3", 20);
KOrderAPI.activeOrderCount(uuid);
```

Every query returns a `CompletableFuture`. Except for `isAvailable()`, every API call may throw `IllegalStateException` when KOrder is unavailable.

`findOrder` returns `CompletableFuture<Optional<OrderSnapshot>>`. Database and I/O failures complete exceptionally.

`ordersByBuyer` returns history, including `ACTIVE`, `COMPLETED`, `CANCELLED`, and `EXPIRED`. `activeOrdersByBuyer` returns only active, unexpired orders.

`searchOrders` returns public, active, unexpired orders. `suggestActiveBuyers` matches usernames case-insensitively. Order query limits are `1..200`; suggestions use `1..45`.

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

`item()` always returns a clone. `active()` is a snapshot check, not a transaction lock.

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

R02-v2 provides no public mutation API for create, cancel, deliver, or payout. This prevents anti-dupe and escrow bypasses.

Queries complete on KOrder's I/O executor. On Folia or Canvas, reschedule entity or world work through your plugin's entity scheduler.
{% endhint %}
