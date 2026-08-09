---
description: Thiết lập phần thưởng Shards theo WorldGuard region.
icon: map-location-dot
---

# WorldGuard region

## WorldGuard region

KShards không tự nhận region. Quản trị viên phải tạo WorldGuard region trước. Sau đó, khai báo rule thủ công.

### Tạo rule

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
Khi thiếu WorldGuard, chỉ thưởng region bị dừng. Số dư và các lệnh KShards khác vẫn hoạt động.
{% endhint %}
