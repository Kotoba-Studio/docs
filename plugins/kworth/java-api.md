---
description: Đọc giá và quote KWorth từ plugin Java khác.
icon: brackets-curly
---

# Java API

## Java API

KWorth đăng ký service để plugin khác đọc giá và quote.

### Lấy `KWorthService`

```java
RegisteredServiceProvider<KWorthService> registration =
        Bukkit.getServicesManager().getRegistration(KWorthService.class);

if (registration == null) {
    return;
}

KWorthService kworth = registration.getProvider();
```

### Lấy quote

```java
SellQuote quote = kworth.quote(player, item);

double base = quote.baseUnitPrice();
double market = quote.marketMultiplier();
double progress = quote.progressionMultiplier();
double total = quote.total();
```

Chỉ dùng API để đọc giá, quote và thông tin liên quan.

{% hint style="warning" %}
Plugin ngoài không nên tự xóa item hoặc payout song song với KWorth.
{% endhint %}
