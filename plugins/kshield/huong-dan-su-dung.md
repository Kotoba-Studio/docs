---
description: Quy trình vận hành KShield, từ kiểm tra rule đến xử lý false positive.
icon: book-open
---

# Hướng dẫn sử dụng

## Hướng dẫn sử dụng

### Kiểm tra sau khi cài

Chạy các lệnh sau sau khi KShield đã khởi động:

```
/kshield rules
/kshield inspect PlayerName
/kshield testmod Meteor
```

`testmod` chỉ kiểm tra registry. Lệnh không gửi probe hoặc kick người chơi.

### Thiết lập phát hiện mod

Thêm rule mới dưới dạng `LOG` trước:

```yaml
mods:
  Meteor:
    severity: LOG
    translations:
      - key.meteor-client.open-gui
```

Theo dõi alert và evidence. Chỉ chuyển sang `KICK` khi fingerprint đã được xác nhận.

### Discord

KShield có hai webhook:

* `alerts`: detection và log.
* `punishments`: kick và ban.

Không chia sẻ webhook URL. Các placeholder hữu ích gồm `%kshield_player%`, `%kshield_blocked_mod_list%` và `%kshield_mod_event_id%`.

### Bedrock và Floodgate

Giữ `bypass-bedrock: true` khi dùng Geyser/Floodgate. Xác minh trạng thái bằng:

```
/kshield inspect PlayerName
```

### Xử lý false positive

1. Chuyển rule sang `LOG`.
2. Chạy `/kshield reload`.
3. Thu thập alert và evidence.
4. Kiểm tra translation hoặc payload gây match.
5. Chỉ khôi phục `KICK` sau khi xác nhận.

### Máy chủ đông người

* Hạn chế fingerprint không cần thiết.
* Giữ `mod-list-limit` thấp.
* Dùng Redis cho cụm nhiều server.
* Theo dõi `/kshield rules` sau mỗi lần reload.

{% hint style="warning" %}
Không dùng `BAN` cho fingerprint chưa kiểm chứng.
{% endhint %}
