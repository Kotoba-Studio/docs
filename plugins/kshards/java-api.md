---
description: Tích hợp KShards trong plugin Java khác.
icon: brackets-curly
---

# Java API

## KShards API

### Dependency

```yaml
softdepend: [KShards]
```

```kotlin
dependencies {
    compileOnly(files("libs/KShards-R1-Release.jar"))
}
```

### Lấy API

```java
import com.konomimc.kshards.api.KShardsAPI;

KShardsAPI shards = Bukkit.getServicesManager().load(KShardsAPI.class);
if (shards == null) return;
```

### Đọc số dư

```java
shards.getBalance(player.getUniqueId()).thenAccept(balance -> {
    getLogger().info("Balance: " + balance);
});
```

### Giao dịch

```java
TransactionContext context = TransactionContext
        .system("MyPlugin", "daily reward")
        .withIdempotencyKey("daily:" + player.getUniqueId() + ":2026-08-09");

shards.add(player.getUniqueId(), 500, context).thenAccept(result -> {
    if (!result.success()) return;
    long balance = result.newBalance();
});
```

{% hint style="warning" %}
Mọi hàm API trả về `CompletableFuture`. Không dùng `.join()` hoặc `.get()` trên main thread.

Chỉ trao phần thưởng sau khi giao dịch trả về thành công.
{% endhint %}
