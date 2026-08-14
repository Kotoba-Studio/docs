---
description: Chẩn đoán lỗi dependency, detection, PlaceholderAPI và reload.
icon: wrench
---

# Khắc phục sự cố

## Khắc phục sự cố

### KShield không load

Kiểm tra PacketEvents. Lỗi thường gặp:

```
UnknownDependencyException: Unknown/missing dependency plugins: [packetevents]
```

Cài PacketEvents đúng bản Bukkit/Paper. Sau đó restart hoàn toàn.

### Kick không hiện mod

Kiểm tra cấu hình:

```yaml
kick-command: "kick %kshield_player% Mod: %kshield_blocked_mod_list%"
```

Sau đó chạy `/kshield reload`.

### Mod không bị detect

Chạy:

```
/kshield testmod <mod>
```

Nếu rule không tồn tại, kiểm tra `mods.yml`. Nếu rule tồn tại, kiểm tra fingerprint `translations` hoặc `payloads`.

### False positive

Chuyển rule sang:

```yaml
severity: LOG
```

Reload, rồi thu thập evidence trước khi đổi lại `KICK`.

### Bedrock bị detect

Cài Floodgate và bật:

```yaml
mod-detection:
  bypass-bedrock: true
```

Kiểm tra lại bằng `/kshield inspect <player>`.

### PlaceholderAPI không nhận

1. Cài PlaceholderAPI.
2. Restart máy chủ.
3. Kiểm tra log đăng ký expansion.
4. Test `%kshield_version%`.
5. Test placeholder player với player context.

### Reload lỗi

Chạy `/kshield reload`, rồi đọc validator trong console. Cấu hình hợp lệ trước đó vẫn tiếp tục chạy.

### Máy chủ đông người

* Hạn chế fingerprint không cần thiết.
* Tránh `BAN` với fingerprint chưa kiểm chứng.
* Dùng Redis cho nhiều backend.
* Giữ database ở latency thấp.
