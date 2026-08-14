---
description: Thiết lập ngôn ngữ, command, storage và rule mod của KShield.
icon: gear
---

# Cấu hình

## Cấu hình

### `config.yml`

#### Ngôn ngữ

```yaml
language: vi_VN
```

`vi_VN` là mặc định. KShield cũng hỗ trợ `en_US`.

#### Lệnh

```yaml
commands:
  base: kshield
  aliases:
    - ks
    - tg
```

Thay đổi command base cần restart.

#### Database và Redis

```yaml
database:
  enabled: false

redis:
  enabled: false
```

Bật database khi cần history hoặc statistics lâu dài. Server đơn thường không cần Redis. Cụm nhiều backend có thể dùng Redis.

#### Bedrock

```yaml
mod-detection:
  bypass-bedrock: true
```

Khuyến nghị bật khi dùng Floodgate.

### `mods.yml`

Rule có thể dùng translation:

```yaml
Meteor:
  severity: KICK
  translations:
    - key.meteor-client.open-gui
```

Hoặc payload:

```yaml
AutoTotem:
  severity: KICK
  payloads:
    - autototem
```

#### Severity

* `LOG`: chỉ ghi nhận.
* `KICK`: kick người chơi.
* `KICK_THEN_BAN`: kick lần đầu, rồi ban khi tái phạm.
* `BAN`: ban ngay.

Dùng `LOG` cho rule mới trước khi chuyển sang `KICK`.

### Kick và ban

```yaml
kick-command: "kick %kshield_player% [KShield] Mod không được phép: %kshield_blocked_mod_list%"
ban-command: "ban %kshield_player% [KShield] Mod không được phép: %kshield_blocked_mod_list%"
```

`%kshield_blocked_mod_list%` chỉ chứa mod gây punishment.

### Áp dụng thay đổi

```
/kshield reload
```

Validator từ chối cấu hình lỗi. Snapshot hợp lệ trước đó tiếp tục chạy.
