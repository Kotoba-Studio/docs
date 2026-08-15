---
description: Thiết lập phần thưởng AFK, rank reward và event multiplier.
icon: map-location-dot
---

# AFK region và event

## AFK region và event

KShards hỗ trợ vùng `CUBOID` và `WORLDGUARD`. WorldGuard cần WorldEdit và region đã tồn tại.

### Tạo rule WorldGuard

```
/kshardsregion set afk world afk 10 1 minutes
/kshardsregion enable afk
```

Ví dụ này trao 10 Shards mỗi phút. Người chơi phải ở region `afk` thuộc world `world`.

### Lệnh

```
/kshardsregion set <id> <world> <region> <amount> <interval> <seconds|minutes|hours>
/kshardsregion enable <id>
/kshardsregion disable <id>
/kshardsregion remove <id>
/kshardsregion list
/kshardsregion reload
```

Quyền sử dụng: `kshards.admin.region`.

{% hint style="info" %}
Khi thiếu WorldGuard, chỉ reward `WORLDGUARD` bị dừng. Số dư và các lệnh khác vẫn hoạt động.
{% endhint %}

### CUBOID và rank reward

CUBOID dùng `pos1`, `pos2` và `world` trong `region-rewards.regions`. Unit hợp lệ: `SECONDS`, `MINUTES`, `HOURS`.

Player cần `kshards.region.earn`, quyền region nếu có, và account không bị chặn. Tránh để region overlap nếu không muốn nhiều reward.

`afk-rank-rewards` tắt mặc định. Rank đầu tiên có permission phù hợp được dùng. `amount` là Shards nhận mỗi lần reward, rồi áp dụng `multiplier` và `bonus`.

### Event multiplier

Dùng `/shards event x2 4m 4d 4h`. Các thời lượng được cộng lại. Giới hạn mặc định là multiplier `100.0` và `365` ngày.

Event lưu nguyên tử vào `events.yml`. Nếu ghi thất bại, state RAM rollback.
